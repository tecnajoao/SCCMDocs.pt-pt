---
title: "Preparar o Intune para a migração de utilizador"
titleSuffix: Configuration Manager
description: "Saiba como preparar o Intune no Azure para a migração de utilizador de híbrida MDM."
keywords: 
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.openlocfilehash: 226586f0ee42cdad98b1d74f25421685d85e0dcf
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/06/2017
---
# <a name="prepare-intune-for-user-migration"></a>Preparar o Intune para a migração de utilizador 

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

Antes de migrar os utilizadores de híbrido (Intune integrado com o Configuration Manager) de MDM ao Intune autónomo, tem de tomar medidas para preparar o Intune. Estes passos ajudam a garantir que os utilizadores migrados e os respetivos dispositivos continuam a ser geridos. Quando concluir estes passos e iniciar a migração para o Intune, deve ser transparente para os seus utilizadores.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Corrija os problemas encontrados durante a importação e recolha de dados
Se Ocorreu o processo de [importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md), a ferramenta do importador de dados do Intune lhe forneceu com um resumo de todos os objetos que não foi possível importar. Alguns dos problemas típicos que, provavelmente, ficou em, bem como passos que pode tomar para corrigir o problema no Intune, estão listados na seguinte tabela: 

|Problema  |Corrigir  |
|---------|---------|
|Coleções com base na associação direcionam ou numa complexas não são ser migradas automaticamente.|Tem de criar grupos do Azure Active Directory (AAD) no Azure para substituir a coleção que não foi importada. Em seguida, tem de atribuir o objeto para o grupo.|
|Não foram importable políticas |Tem de recriar a política no Intune.|
|Implementação de um objeto importado|Tem de atribuir o objeto para o grupo. O grupo deve conter os mesmos utilizadores da coleção para a implementação.|

## <a name="create-intune-objects"></a>Criar objetos do Intune 
Se Ocorreu o processo de [importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md) e corrigir problemas durante o processo de importação, deve verificar os objetos importados estão corretamente configurados. Além disso, crie quaisquer objetos adicionais (políticas, perfis, aplicações, etc.) no Intune que precisa na sua organização. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Atribuir licenças do Intune aos utilizadores migrados
No Configuration Manager, adicionar uma coleção para a subscrição do Intune e os membros da coleção têm a capacidade de inscrever os respetivos dispositivos. Enquanto uma licença do Intune está reservada para dispositivos inscritos, estes licenças não são especificamente associadas ao utilizador ou dispositivo. Por exemplo, não encontrará uma licença do Intune no AAD para um utilizador que tem um dispositivo inscrito. No entanto, Intune autónomo tem de configurar uma licença do Intune para cada utilizador. Deve fazê-lo antes de migrar um utilizador para o Intune autónomo para se certificar de que o utilizador e os respetivos dispositivos são geridos pelo Intune após a alteração na autoridade de MDM. Para obter mais informações, consulte [licenças do Intune atribuir às suas contas de utilizador](https://docs.microsoft.com/intune/licenses-assign). 

## <a name="verify-intune-user-groups"></a>Certifique-se grupos de utilizadores do Intune
Os utilizadores e grupos são provável que já no AAD porque tiver configurada a sincronização de diretórios. Para se certificar de que os utilizadores fazem parte do grupo de utilizador correto, recomendamos que reveja os grupos de utilizadores do Intune. O direcionamento políticas, perfis, aplicações, etc. para estes grupos. Certifique-se os utilizadores a que migrar para o Intune autónomo parte dos grupos de corretos. 

## <a name="configure-role-based-administration-control-rbac"></a>Configurar o controlo de administração baseada em funções (RBAC)
Como parte da migração, configure todas as funções de RBAC necessários no Intune e atribuir utilizadores a essas funções. Tenha em atenção que existem diferenças entre o RBAC no Configuration Manager e o Intune, tais como âmbito de recursos. Para obter mais informações, consulte [o controlo de administração baseada em funções (RBAC) com o Intune](https://docs.microsoft.com/en-us/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Atribuir políticas de aplicações e aos grupos de AAD
Se ocorreu de [Gestor de configuração da importação de dados para o Microsoft Intune](migrate-import-data.md) fase do processo de migração para migrar o Gestor de configuração diferentes objetos para o Intune, muitos dos seus objetos possam ser atribuídos a grupos do AAD. No entanto, deve verificar que todos os objetos (aplicações, políticas, perfis, etc.) estão atribuídos a grupos AAD corretos. Se atribuir objetos corretamente, dispositivos do utilizador são configurados automaticamente depois do utilizador é migrado e da migração deve ser transparente para os utilizadores. Para obter detalhes sobre a atribuição de objetos a um grupo do AAD, consulte o seguinte: 
- [Atribuir políticas](https://docs.microsoft.com/intune/get-started-policies) 
- [Atribuir perfis](https://docs.microsoft.com/intune/device-profile-assign) 
- [Atribuir as aplicações](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Política de termos e condições
Tal como outras políticas ao nível do inquilino, políticas de termos e condições são migradas automaticamente para o Intune quando a autoridade mista estiver ativada para o seu inquilino.  No entanto, tem de atribuir os termos e condições para um grupo que contenha migrados os utilizadores com precisão relatórios sobre a aceitação de utilizadores migrados e certifique-se de que os termos e condições corretamente como destino de termos de licenciamento futuros e atualizações de condições ou dispositivo inscrições. Não é necessário que os utilizadores voltem a aceitar os termos e condições, exceto se existem alterações efetuadas para a política na consola do Configuration Manager. Para obter mais informações, consulte [atribuir termos e condições](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configurar o conector do Exchange
Se utilizar o Exchange e tiver um conector do Exchange no local no Configuration Manager, terá de [configurar o conector do Exchange no local no Intune](https://docs.microsoft.com/intune/exchange-connector-install). Considere também as informações nas secções seguintes para ajudar a migrar para o Intune Exchange Connector e certifique-se de trabalho de acesso condicional corretamente após a migração.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Scripts do PowerShell para o ajudar a migrar para o Intune Exchange Connector 
Scripts do PowerShell estão disponíveis para o ajudar a preparar para transitar os dispositivos do Exchange do conector do Exchange do Configuration Manager para o Intune Exchange Connector. Ao ser executado estes scripts são opcionais, que recomendamos que execute-los para remover dispositivos Inativos do Exchange, o que impede que o Intune detetar dispositivos de desnecessários. Executar os scripts Certifique-se de que os dispositivos detetados através do Exchange podem intercalar com dispositivos inscritos com o Intune facilmente quanto possível. Execute estes scripts antes de configurar o Intune Exchange Connector. Os scripts do PowerShell fazem parte da instalação do importador de dados do Intune que utiliza para [importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md) no seguinte artigo. Para obter mais informações e para transferir os scripts, aceda a [importador de dados do Microsoft Intune](https://github.com/ConfigMgrTools/Intune-Data-Importer) página do GitHub.

### <a name="steps-to-ensure-conditional-access-works-properly-after-user-migration"></a>Passos para garantir o acesso condicional funciona corretamente após a migração de utilizador
Acesso condicional para funcionar corretamente depois de migrar utilizadores e para garantir que os utilizadores continuam a ter acesso ao respetivo servidor de e-mail, certifique-se de que as seguintes condições for verdadeira:
- Se o Exchange ActiveSync acesso nível predefinição (DefaultAccessLevel) estiver definida como bloquear ou colocar em quarentena, dispositivos poderão perder o acesso ao e-mail. 
- Se o conector do Exchange estiver instalado no Configuration Manager e o **nível de acesso quando um dispositivo móvel não é gerido por uma regra** definição tem um valor de **permitir o acesso**, tem de instalar o [ Conector do Exchange no local](https://docs.microsoft.com/en-us/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) no Intune antes de migrar os utilizadores. Configure a definição de nível de acesso predefinida no Intune no **Exchange no local** painel no **as definições de acesso do Exchange ActiveSync avançadas**. Para obter mais informações, consulte [configurar o Exchange no local acesso](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Utilize a mesma configuração para os dois conectores. O conector do último que configurar substitui as definições de organização ActiveSync anteriormente escritas pelo conector do outro. Se configurar os conectores de forma diferente, pode resultar em alterações de acesso condicional inesperado.
- Remova utilizadores de filtragem de acesso condicional no Configuration Manager depois de serem migradas para o Intune autónomo.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configurar o Microsoft Intune Certificate Connector
Se utilizar o NDES para emitir certificados utilizem SCEP, terá de configurar o Microsoft Intune Certificate Connector. O computador que aloja o conector do NDES no Intune não pode ser o mesmo computador que aloja o conector do NDES no Configuration Manager. Para obter mais informações, consulte [configurar e gerir certificados SCEP com o Intune](https://docs.microsoft.com/en-us/intune/certificates-scep-configure). 

> [!Important]    
> Depois de configurar o conector, tem de modificar perfis SCEP importados para o novo URL do servidor de referência.

## <a name="next-step"></a>Passo seguinte
Depois de preparar o Intune para a migração, está pronto para migrar um conjunto de utilizadores de teste para o Intune autónomo. Para obter mais informações, consulte [alterar a autoridade de MDM para utilizadores específicos (misturadas autoridade)](migrate-mixed-authority.md).


