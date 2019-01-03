---
title: Preparar o Intune para a migração de utilizadores
titleSuffix: Configuration Manager
description: Saiba como preparar o Intune no Azure para a migração de utilizador da híbrida MDM.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/26/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.openlocfilehash: f7c0f0d9dc52c39e0ec33abb8df565d4918471f7
ms.sourcegitcommit: 54e5786875c4e5f5c1b54e38ed59e96344faf9b4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/02/2019
ms.locfileid: "53818043"
---
# <a name="prepare-intune-for-user-migration"></a>Preparar o Intune para a migração de utilizadores 

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    
Antes de migrar os utilizadores da MDM híbrida para o Intune autónomo, executar etapas para preparar o Intune. Estes passos ajudam a tornar-se de que os utilizadores migrados e os respetivos dispositivos continuam a ser geridos. Quando concluir estes passos e iniciar a migração para o Intune, não há nenhum impacto signifcant aos seus utilizadores.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Corrigir problemas encontrados durante a importação e a recolha de dados
Se utilizou a ferramenta importador de dados do Intune para [importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md), ele resumidos os objetos que não foi possível importar. Alguns dos problemas comuns e passos para corrigi-los no Intune, estão listados na tabela a seguir: 

|Problema  |Corrigir  |
|---------|---------|
|Coleções com base na associação direta ou num complexo não são migradas automaticamente.|Crie grupos do Azure Active Directory (Azure AD) no Azure para substituir a coleção que não foi importada. Em seguida, atribua o objeto para o grupo.|
|As políticas não eram importável |Recrie a política no Intune.|
|Implementação de um objeto não importado|Atribua o objeto ao grupo. O grupo deve incluir os mesmos utilizadores da coleção para a implementação.|

## <a name="create-intune-objects"></a>Criar objetos do Intune 
Se [importados dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md) e foram corrigidos erros durante o processo, certifique-se os objetos importados estão corretamente configurados. Também crie todos os objetos adicionais (políticas, perfis e aplicações) do Intune que tem na sua organização. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Atribuir licenças do Intune para utilizadores migrados
No Configuration Manager, adiciona uma coleção para a subscrição do Intune e os membros da coleção podem inscrever os respetivos dispositivos. Embora uma licença do Intune está reservada para dispositivos inscritos, estas licenças não estão associadas ao utilizador ou dispositivo. Por exemplo, não encontrar uma licença do Intune no Azure AD para um utilizador com um dispositivo inscrito. 

No Intune autónomo, configure uma licença do Intune para cada utilizador. Configurar a licença *antes de* migrar um utilizador para o Intune autónomo. Esta ação torna-se de que o utilizador e os respetivos dispositivos são geridos pelo Intune após a alteração da autoridade de MDM. Para obter mais informações, veja [Atribuir licenças do Intune às suas contas de utilizador](https://docs.microsoft.com/intune/licenses-assign). 

## <a name="verify-intune-user-groups"></a>Certifique-se de grupos de utilizadores do Intune
Os utilizadores e grupos são provável que já no Azure AD uma vez que tiver configurada a sincronização de diretórios. Para certificar-se de que os utilizadores fazem parte do grupo de utilizadores correto, recomendamos que reveja os grupos de utilizadores do Intune. O direcionamento de políticas, perfis e aplicações a estes grupos. Certifique-se de que os utilizadores a que migrar para o Intune autónomo fazem parte dos grupos de corretos. 

## <a name="configure-role-based-administration-control-rbac"></a>Configurar o controlo de administração baseada em funções (RBAC)
Como parte da migração, configure todas as funções RBAC necessárias no Intune e atribuir utilizadores a essas funções. Existem diferenças entre o RBAC no Configuration Manager e o Intune, como o âmbito de recursos. Para obter mais informações, consulte [controlo de administração baseada em funções (RBAC) com o Intune](https://docs.microsoft.com/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Atribuir aplicações e políticas a grupos do AAD
Se [importados dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md), muitos dos seus objetos já poderão ser atribuídos a grupos do Azure AD. Certifique-se de que todos os objetos (aplicações, políticas e perfis) estão atribuídos a correta para grupos do Azure AD. Se atribuir objetos corretamente, dispositivos do utilizador são configurados automaticamente depois do utilizador é migrado e a migração não deve ter qualquer impacto signifcant para os utilizadores. Para obter mais informações sobre a atribuição de objetos a um grupo do Azure AD, consulte os artigos seguintes: 
- [Atribuir políticas](https://docs.microsoft.com/intune/get-started-policies)  
- [Atribuir perfis](https://docs.microsoft.com/intune/device-profile-assign)  
    > [!NOTE]  
    > Quando o Intune implementa o novo perfil de e-mail, os utilizadores recebem uma linha de comandos de reintroduzir a palavra-passe.  
- [Atribuir aplicações](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Política de termos e condições
Assim como outras políticas ao nível do inquilino, políticas de termos e condições são migradas automaticamente para o Intune quando a autoridade mista estiver ativada para o seu inquilino.  No entanto, tem de atribuir os termos e condições para um grupo que contenha migrados que os utilizadores com precisão o relatório de aceitação para os utilizadores migrados e certifique-se de que os termos e condições corretamente são direcionadas para termos futuros e atualizações de condições ou dispositivo inscrições. Os utilizadores não têm voltem os termos e condições, a menos que haja alterações feitas à política na consola do Configuration Manager. Para obter mais informações, consulte [atribuir termos e condições](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configurar o conector do Exchange
Se utilizar o Exchange e tiver um conector do Exchange no local no Configuration Manager, terá [configurar o conector do Exchange no local no Intune](https://docs.microsoft.com/intune/exchange-connector-install). Considere também as informações nas secções seguintes para ajudar a migrar para o Exchange Connector do Intune e para se certificar de que o acesso condicional funciona corretamente após a migração.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Scripts do PowerShell para o ajudar a migrar para o Exchange Connector do Intune 
Scripts do PowerShell estão disponíveis para o ajudar a preparar para fazer a transição de seus dispositivos de Exchange a partir do Configuration Manager Exchange Connector para o Exchange Connector do Intune. Ao executar estes scripts estão opcionais, que recomendamos que executá-los para remover dispositivos Inativos do Exchange, o que impede que o Intune detetar dispositivos de desnecessários. Executar os scripts Certifique-se de que os dispositivos detetados através do Exchange podem intercalar com dispositivos inscritos no Intune, o mais tranqüila possível. Execute estes scripts antes de configurar o Intune Exchange Connector. Os scripts do PowerShell fazem parte da instalação importador de dados do Intune que utilizar para [importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md) no próximo artigo. Para obter detalhes e para transferir os scripts, aceda a [importador de dados do Microsoft Intune](https://github.com/ConfigMgrTools/Intune-Data-Importer) página do GitHub.

### <a name="steps-to-make-sure-conditional-access-works-properly-after-user-migration"></a>Passos para garantir o acesso condicional-se de que funciona corretamente após a migração de utilizador
Para obter acesso condicional para funcionar corretamente depois de migrar utilizadores e certifique-se de que os utilizadores continuam a ter acesso ao respetivo servidor de e-mail, certificar-se de que são definidas as seguintes configurações:
- Se o Exchange ActiveSync acesso nível predefinição (da organização) é definida como bloqueio ou quarentena, dispositivos poderão perder o acesso ao e-mail. 
- Se o conector do Exchange estiver instalado no Configuration Manager e o **quando um dispositivo móvel não é gerido por uma regra de nível de acesso** definição tem um valor de **permitir o acesso**, instalar o [ Conector do Exchange no local](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) no Intune antes de migrar os utilizadores. Configurar a definição de nível de acesso predefinida no Intune no **Exchange no local** página no **definições de acesso do Advanced Exchange ActiveSync**. Para obter mais informações, consulte [configurar o Exchange no local acesso](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Utilize a mesma configuração para os dois conectores. O conector do último que configurar substitui as definições de organização do ActiveSync já gravadas pelo conector do outro. Se configurar os conectores de forma diferente, pode resultar em alterações de acesso condicional inesperado.
- Remova utilizadores de acesso condicional direcionamento no Configuration Manager, uma vez que eles são migrados para o Intune autónomo.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configurar o Microsoft Intune Certificate Connector
Se usar o NDES para emitir certificados através de SCEP, tem de configurar o Microsoft Intune Certificate Connector. O computador que aloja o conector do NDES no Intune não pode ser o mesmo computador que aloja o conector do NDES no Configuration Manager. Para obter mais informações, consulte [configurar e gerir certificados SCEP com o Intune](https://docs.microsoft.com/intune/certificates-scep-configure). 

> [!Important]    
> Depois de configurar o conector, modificar importados perfis SCEP para referenciar o novo URL do servidor.

## <a name="next-step"></a>Passo seguinte
Depois de preparar o Intune para a migração, está pronto para migrar um conjunto de utilizadores de teste para o Intune autónomo. Para obter mais informações, consulte [alterar a autoridade MDM para utilizadores específicos (autoridade misturadas)](migrate-mixed-authority.md).


