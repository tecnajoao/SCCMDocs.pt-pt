---
title: Criar perfis de ligação remota
titleSuffix: Configuration Manager
description: Utilize perfis de ligação remota do System Center Configuration Manager para permitir que os utilizadores liguem remotamente a computadores de trabalho.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 7d6bcb46650082cebc95e8300a2f6adeb119fdbf
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421880"
---
# <a name="remote-connection-profiles-in-system-center-configuration-manager"></a>Perfis de ligação remota no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Perfis de ligação remota do Configuration Manager utilizar o Centro de sistema para permitir que os utilizadores liguem remotamente a computadores de trabalho quando não estiverem ligados ao domínio ou se os seus computadores pessoais estiverem ligados através da Internet.  

 Os utilizadores podem ligar-se aos seus PC de trabalho a partir dos seguintes tipos de dispositivos:  

-   Computadores com o Microsoft Windows  

-   Dispositivos com iOS  

-   Dispositivos com Android  

Perfis de ligação remota permitem-lhe implementar definições de ligação de ambiente de trabalho remota aos utilizadores na sua hierarquia do Configuration Manager. Os utilizadores podem depois utilizar o portal da empresa para aceder a qualquer computador de trabalho primário através do Ambiente de Trabalho Remoto, utilizando as definições de Ligação ao Ambiente de Trabalho Remoto fornecidas pelo portal.  

O Microsoft Intune é necessário se pretender que os utilizadores liguem aos seus computadores de trabalho através do portal da empresa. Se não estiver a utilizar o Intune, os utilizadores continuam a poder utilizar as informações do perfil de ligação remota para ligar aos seus PC de trabalho, utilizando o Ambiente de Trabalho Remoto através de uma ligação VPN.  

> [!IMPORTANT]  
>  Quando especifica definições de perfil de ligação remota utilizando a consola do Configuration Manager, as configurações são armazenadas na política local do computador cliente. Estas definições podem substituir as definições de Ambiente de Trabalho Remoto configuradas por outra aplicação. Além disso, se utilizar a política de grupo do Windows para configurar as definições de ambiente de trabalho remoto, as definições especificadas na política de grupo substituirão as configuradas através do Configuration Manager.  

 Ao instalar o Configuration Manager, um novo grupo de segurança, **ligação ao PC remoto**, é criado. Este grupo é preenchido quando é implementado um perfil de ligação remota que inclui os utilizadores primários do computador em que o perfil é implementado. Embora um administrador local possa adicionar nomes de utilizadores a este grupo, esses utilizadores serão removidos do grupo na próxima vez que for avaliada a compatibilidade dos perfis de ligação remota implementados.  

 Se adicionar manualmente um utilizador a este grupo, o utilizador pode iniciar ligações remotas, mas a informação da ligação não será publicada no portal da empresa.  

 Se remover manualmente do grupo de um utilizador que tenha sido adicionado pelo Configuration Manager, Configuration Manager irá remediar automaticamente esta alteração ao adicionar o utilizador de volta quando o perfil de ligação remota é o próximo avaliados quanto à conformidade.  

> [!IMPORTANT]  
>  Se a relação de afinidade de dispositivo do utilizador entre um utilizador e um dispositivo é alterado (por exemplo, o computador de um usuário se conecta ao, deixa de ser um dispositivo primário do utilizador, o Configuration Manager desativa o perfil de ligação remota e as definições da Firewall do Windows impedi ligações ao computador.  

## <a name="prerequisites"></a>Pré-requisitos  

### <a name="external-dependencies"></a>Dependências externas  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Servidor de Gateway de Ambiente de Trabalho Remoto.|Se pretender permitir que os utilizadores estabeleçam ligação à Internet fora do domínio da empresa, terá de instalar e configurar um servidor de Gateway de Ambiente de Trabalho remoto.<br /><br /> Se as definições do Ambiente de Trabalho Remoto ou dos Serviços de Terminal forem geridas por outra aplicação ou pelas definições de Política de Grupo, os perfis de ligação remota poderão não funcionar corretamente. Ao implementar perfis de ligação remota a partir da consola do Configuration Manager, as respetivas definições são armazenadas na política local do computador cliente. Estas definições poderão substituir as definições de Ambiente de Trabalho Remoto configuradas por outra aplicação. Além disso, se utilizar definições de política de grupo para configurar as definições de ambiente de trabalho remoto, as definições que são especificadas nas definições de política de grupo substituirão as definições são configuradas pelo Configuration Manager.<br /><br /> Para mais informações sobre como instalar e configurar um servidor de Gateway de Ambiente de Trabalho Remoto, consulte a documentação do Windows Server.|  
|Se os computadores cliente executarem uma firewall baseada no anfitrião, terão de ativar o programa Mstsc.exe.|Quando configura um perfil de ligação remota, tem de ativar a definição **Permitir exceção de Firewall do Windows para ligações em domínios do Windows e em redes privadas** . Quando esta definição estiver ativada, o Configuration Manager configura automaticamente a Firewall do Windows para ativar o programa Mstsc.exe. No entanto, se os computadores cliente executarem outra firewall baseada no anfitrião, terá de configurar manualmente esta dependência de firewall.<br /><br /> As definições de Política de Grupo para configurar a Firewall do Windows poderão substituir a configuração definida no Configuration Manager. Se utilizar a Política de Grupo para configurar a Firewall do Windows, certifique-se de que as definições de Política de Grupo não bloqueiam o programa Mstsc.exe.|  

### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|O Configuration Manager tem de estar ligado ao Microsoft Intune (conhecido como configuração híbrida).|Para obter mais informações sobre como ligar o Configuration Manager para o Microsoft Intune, veja gerir dispositivos móveis com o Configuration Manager e o Microsoft Intune.|  
|Para que um utilizador possa ligar a um computador de trabalho na rede da empresa, esse computador terá de ser um dispositivo primário do utilizador.|Para obter mais informações sobre a afinidade de dispositivo do utilizador, consulte [associar utilizadores e dispositivos à afinidade dispositivo / utilizador](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).|  
|Deverão ter sido concedidas permissões de segurança específicas para gerir perfis de ligação remota.|A função de segurança **Gestor de Definições de Conformidade** inclui as permissões necessárias para gerir os perfis de ligação remota. Para obter mais informações, veja <br />[Configurar a administração baseada em funções](/sccm/core/servers/deploy/configure/configure-role-based-administration).|  

## <a name="security-and-privacy-considerations-for-remote-connection-profiles"></a>Considerações de segurança e privacidade para perfis de ligação remota  

### <a name="security-considerations"></a>Considerações de segurança  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Especifique manualmente a afinidade dispositivo/utilizador em vez de permitir que os utilizadores identifiquem o respetivo dispositivo primário. Além disso, não ative a configuração baseada na utilização.|Uma vez que tem de ativar a opção **Permitir a todos os utilizadores primários do computador de trabalho ligar de forma remota** para poder implementar um perfil de ligação remota, especifique sempre manualmente a afinidade dispositivo/utilizador. Não considere autoritativas as informações recolhidas junto dos utilizadores ou do dispositivo. Se implementar perfis de ligação remota e um utilizador administrativo fidedigno não especificar a afinidade dispositivo/utilizador, os utilizadores não autorizados poderão obter privilégios elevados, sendo capazes de estabelecer ligação remota aos computadores.<br /><br /> Se ativar a configuração baseada na utilização, estas informações serão obtidas por meio de mensagens de estado para o qual o Configuration Manager não fornece segurança. Para ajudar a atenuar esta ameaça, utilize a assinatura de Bloco de Mensagem de Servidor (SMB) ou o protocolo IPsec (Internet Protocol Security) entre os computadores cliente e o ponto de gestão.|  
|Restrinja os direitos administrativos locais no computador do servidor de site.|Um utilizador que tenha direitos administrativos locais no servidor do site pode adicionar manualmente membros ao grupo de segurança ligação ao PC remoto do Configuration Manager automaticamente cria e mantém. Isto poderá provocar uma elevação de privilégios, uma vez que os membros que são adicionados a este grupo recebem permissões de Ambiente de Trabalho Remoto.|  

### <a name="privacy-considerations"></a>Considerações de privacidade  

-   Se um utilizador iniciar uma ligação a um computador de trabalho a partir do portal da empresa, será transferido um ficheiro com extensão .rdp ou .wsrdp, contendo o nome do dispositivo e o nome do Servidor de Gateway de Ambiente de Trabalho Remoto necessário para iniciar a sessão do Ambiente de Trabalho Remoto. A extensão do ficheiro depende do sistema operativo do dispositivo. Por exemplo, os sistemas operativos Windows 7 e Windows 8 utilizam um ficheiro .rdp, e o Windows 8.1 utiliza um ficheiro .wsrdp.  

-   O utilizador poderá optar por abrir ou guardar o ficheiro .rdp. Se o utilizador optar por abrir o ficheiro .rdp, o ficheiro poderá ser armazenado na cache do browser, conforme as definições de retenção configuradas no browser. Se o utilizador optar por guardar o ficheiro, o ficheiro não será armazenado na cache do browser. O ficheiro será guardado até que o utilizador o elimine manualmente.  

-   O ficheiro .wsrdp é transferido e guardado localmente, de forma automática. O ficheiro será substituído da próxima vez que o utilizador executar uma sessão de Ambiente de Trabalho Remoto.  

-   Antes de configurar os perfis de ligação remota, considere os requisitos de privacidade.  


## <a name="create-a-remote-connection-profile"></a>Criar um perfil de ligação remota

1. Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **perfis de ligação remota**.  

2. No separador **Home Page** , no grupo **Criar** , clique em **Criar Perfil de Ligação Remota**.  

3. Na página **Geral** do **Assistente para Criar Perfil de Ligação Remota**, especifique um nome e uma descrição opcional para o perfil com um máximo de 256 carateres para cada um.  

4. Sobre o **perfil** página Definições, especifique as seguintes definições para o perfil de ligação remota:  

   -   **Nome completo e porta do servidor de Gateway de Ambiente de Trabalho Remoto (opcional)** - especifique o nome do Servidor de Gateway de Ambiente de Trabalho Remoto para ser utilizado nas ligações.  

       > [!NOTE]  
       >  O Configuration Manager não suporta um nome de domínio internacionalizado para ser utilizado para especificar um servidor nesta caixa.  
       >   
       >  O nome do servidor não deve exceder os 256 carateres e pode conter carateres maiúsculos, carateres minúsculos, carateres numéricos e os carateres **–** e **_** , separados por pontos.  

   -   **Permitir ligações apenas de computadores que executem o Ambiente de Trabalho Remoto com Autenticação de Nível de Rede**  

5. Selecione **Ativado** ou **Desativado** para cada uma das seguintes definições de ligação:  

   -   **Permitir ligações remotas a computadores de trabalho**  

   -   **Permitir a ligação remota de todos os utilizadores primários do computador de trabalho**  

   -   **Permitir exceção da Firewall do Windows para ligações em domínios do Windows e em redes privadas**  

   > [!IMPORTANT]  
   >  As três definições têm de ser idênticas para poder passar esta página do assistente.  

6. Sobre o **resumo** página, reveja as ações a executar e, em seguida, conclua o assistente.  

   O novo perfil de ligação remota é apresentado no nó **Perfis de Ligação Remota** da área de trabalho **Ativos e Compatibilidade** .  

Implementar um perfil de ligação remota  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **perfis de ligação remota**.  

3.  Na lista **Perfis de Ligação Remota** , selecione o perfil de ligação remota que pretende implementar e, no separador **Home Page** do grupo **Implementação** , clique em **Implementar**.  

4.  Na caixa de diálogo **Implementar Perfil de Ligação Remota** , especifique as seguintes informações:  

    -   **Coleção** - Clique em **Procurar** para selecionar a coleção de dispositivos onde pretende implementar o perfil de ligação remota.  

    -   **Remediar regras incompatíveis quando suportado** -ative esta opção para retificar automaticamente o perfil de ligação remota quando não for compatível num dispositivo, por exemplo, quando não estiver presente.  

    -   **Permitir remediação fora da janela de manutenção** - se uma janela de manutenção tiver sido configurada para a coleção em que pretende implementar o perfil de ligação remota, ative esta opção permitir que o Configuration Manager remediar a ligação remota perfil fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  

    -   **Gerar um alerta** - Ative esta opção para configurar um alerta que será gerado se a compatibilidade do perfil de ligação remota for inferior a uma determinada percentagem num data e hora especificadas. Também pode especificar se pretende que seja enviado um alerta para o System Center Operations Manager.  

    -   **Especifique o agendamento de avaliação de compatibilidade para esta linha de base de configuração** - Especifique a agenda para avaliação do perfil de ligação remota implementado nos dispositivos. É possível especificar uma agenda simples ou personalizada.  

    > [!TIP]  
    >  Se um dispositivo deixa uma coleção na qual foi implementado um perfil de ligação remota, as definições do perfil de ligação remota são desativadas no dispositivo. No entanto, para que este processo decorra corretamente, deve ter implementado pelo menos um item de configuração ou uma linha de base de configuração que contenha um item de configuração do site.  
    >   
    >  O perfil é avaliado por dispositivos quando o utilizador inicia sessão.  
    >   
    >  Se forem implementados dois perfis de ligação remota na mesma coleção de dispositivos, estando selecionada a opção **Remediar regras incompatíveis quando suportado** num dos perfis e desativada no outro, e se os dois perfis de ligação remota contiverem definições de ligação diferentes, o perfil com a opção desativada pode substituir as definições do outro perfil. Este tipo de implementação de perfil de ligação remota não é suportado pelo Configuration Manager.  

5.  Clique em **OK** para fechar a caixa de diálogo **Implementar Perfil de Ligação Remota** e criar a implementação.  

## <a name="monitor-a-remote-connection-profile"></a>Monitorizar um perfil de ligação remota  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Ver os resultados de compatibilidade na consola do Configuration Manager  

1.  Na consola do Configuration Manager, clique em **monitorização** > **implementações**.  

3.  Na lista **Implementações** , selecione a implementação de perfil de ligação remota cujas informações de compatibilidade pretende rever.  

4.  Poderá rever as informações de resumo sobre a conformidade da implementação do perfil de ligação remota na página principal. Para ver informações mais detalhadas, selecione a implementação de perfil de ligação remota e, no separador **Home Page** , no grupo **Implementação** , clique em **Ver Estado** para abrir a página **Estado da Implementação** .  

     A página **Estado da Implementação** contém os seguintes separadores:  

    -   **Em conformidade:** Apresenta a compatibilidade do perfil de ligação remota com base no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário no nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** . Este nó contém todos os dispositivos compatíveis com o perfil de ligação remota. O painel **Detalhes do Ativo** também apresenta os dispositivos que são compatíveis com este perfil. Faça duplo clique num dispositivo da lista para visualizar informações adicionais.  

        > [!IMPORTANT]  
        >  Um perfil de ligação remota não é avaliado se não for aplicável num dispositivo cliente. No entanto, é devolvido como compatível.  

    -   **Erro:** Apresenta uma lista de todos os erros para a implementação de perfil de ligação remota selecionado com base no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário no nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** . Este nó contém todos os dispositivos que geraram erros com este perfil. Quando um dispositivo é selecionado, o painel **Detalhes do Ativo** apresenta os dispositivos que o problema selecionado afeta. Faça duplo clique num dispositivo da lista para visualizar informações adicionais sobre o problema.  

    -   **Não compatível:** Apresenta uma lista de todas as regras não compatíveis no perfil de ligação remota com base no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário no nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** . Este nó contém todos os dispositivos que não são compatíveis com este perfil. Quando um dispositivo é selecionado, o painel **Detalhes do Ativo** apresenta os dispositivos que o problema selecionado afeta. Faça duplo clique num dispositivo da lista para visualizar informações adicionais sobre o problema.  

    -   **Desconhecido:** Apresenta uma lista de todos os dispositivos que não comunicaram compatibilidade para a implementação de perfil de ligação remota selecionado, juntamente com o estado atual do cliente dos dispositivos.  

5.  Na página **Estado da Implementação** , poderá rever informações detalhadas sobre a compatibilidade do perfil de ligação remota implementado. É criado um nó temporário no nó **Implementações** que o ajuda a localizar novamente estas informações de forma rápida.  

### <a name="view-compliance-results-with-reports"></a>Ver resultados de compatibilidade com relatórios  
 O Configuration Manager inclui relatórios incorporados que pode utilizar para monitorizar informações sobre perfis de ligação remota. Estes relatórios têm a categoria de relatório de **Gestão de Compatibilidade e Definições**.  

> [!IMPORTANT]  
>  Deverá utilizar um caráter universal (%) ao utilizar os parâmetros **Filtro do dispositivo** e **Filtro do utilizador** nos relatórios de definições de compatibilidade.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [relatórios no System Center Configuration Manager](/sccm/core/servers/manage/reporting).  
