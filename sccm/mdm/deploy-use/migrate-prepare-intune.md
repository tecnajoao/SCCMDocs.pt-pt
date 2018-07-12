---
title: Preparar o Intune para a migração de utilizador
titleSuffix: Configuration Manager
description: Saiba como preparar o Intune no Azure para a migração de utilizador da híbrida MDM.
author: aczechowski
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.openlocfilehash: 0d71abbe33def6e12e75c2042e48f3d7ddcfe5c6
ms.sourcegitcommit: 06d490d526070e17d77e86bc6c200899ded911cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/11/2018
ms.locfileid: "38967152"
---
# <a name="prepare-intune-for-user-migration"></a>Preparar o Intune para a migração de utilizador 

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

Antes de migrar os utilizadores da MDM (Intune integrado com o Configuration Manager) híbrida para o Intune autónomo, tem de seguir passos para preparar o Intune. Estes passos ajudam a garantir que os utilizadores migrados e os respetivos dispositivos continuam a ser geridos. Quando concluir estes passos e iniciar a migração para o Intune, deve ser transparente aos seus utilizadores.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Corrigir problemas encontrados durante a importação e a recolha de dados
Se fosse o processo de [importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md), a ferramenta importador de dados do Intune fornecido a um resumo de todos os objetos que não foi possível importar. Alguns dos problemas típicos que provavelmente foi executado em, bem como passos que pode tomar para corrigir o problema no Intune, estão listados na tabela a seguir: 

|Problema  |Corrigir  |
|---------|---------|
|Coleções com base na associação direta ou num complexo não são ser migradas automaticamente.|Tem de criar grupos do Azure Active Directory (AAD) no Azure para substituir a coleção que não foi importada. Em seguida, tem de atribuir o objeto para o grupo.|
|As políticas não eram importável |Tem de recriar a política no Intune.|
|Implementação de um objeto não importado|Tem de atribuir o objeto para o grupo. O grupo deve conter os mesmos utilizadores da coleção para a implementação.|

## <a name="create-intune-objects"></a>Criar objetos do Intune 
Se fosse o processo de [importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md) e foram corrigidos erros durante o processo de importação, deve verificar os objetos importados estão corretamente configurados. Além disso, crie todos os objetos adicionais (políticas, perfis, aplicações, etc.) no Intune que precisa na sua organização. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Atribuir licenças do Intune para utilizadores migrados
No Configuration Manager, adiciona uma coleção para a subscrição do Intune e os membros da coleção tem a capacidade de inscrever os respetivos dispositivos. Embora uma licença do Intune está reservada para dispositivos inscritos, estas licenças não são especificamente associadas ao utilizador ou dispositivo. Por exemplo, não encontrar uma licença do Intune no AAD para um utilizador com um dispositivo inscrito. No entanto, no Intune autónomo tem de configurar uma licença do Intune para cada utilizador. Tem de o fazer antes de migrar um utilizador para o Intune autónomo para se certificar de que o utilizador e os respetivos dispositivos são geridos pelo Intune após a alteração da autoridade de MDM. Para obter mais informações, consulte [atribuir licenças do Intune às contas de utilizador](https://docs.microsoft.com/intune/licenses-assign). 

## <a name="verify-intune-user-groups"></a>Certifique-se de grupos de utilizadores do Intune
Os utilizadores e grupos são provável que já no AAD uma vez que tiver configurada a sincronização de diretórios. Para certificar-se de que os utilizadores fazem parte do grupo de utilizadores correto, recomendamos que reveja os grupos de utilizadores do Intune. O direcionamento de políticas, perfis, aplicações, etc. a esses grupos. Certifique-se de que os utilizadores a que migrar para o Intune autónomo fazem parte dos grupos de corretos. 

## <a name="configure-role-based-administration-control-rbac"></a>Configurar o controlo de administração baseada em funções (RBAC)
Como parte da migração, configure todas as funções RBAC necessárias no Intune e atribuir utilizadores a essas funções. Tenha em atenção que existem diferenças entre o RBAC no Configuration Manager e o Intune, como o âmbito de recursos. Para obter detalhes, consulte [controlo de administração baseada em funções (RBAC) com o Intune](https://docs.microsoft.com/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Atribuir aplicações e políticas a grupos do AAD
Se percorreu a [Gestor de configuração da importação de dados para o Microsoft Intune](migrate-import-data.md) fase do processo de migração para migrar o Gestor de configuração diferentes de objetos para o Intune, muitos dos seus objetos já poderão ser atribuídos a grupos do AAD. No entanto, deve verificar que todos os objetos (aplicações, políticas, perfis, etc.) são atribuídos a grupos do AAD corretos. Se atribuir objetos corretamente, dispositivos do utilizador são configurados automaticamente depois do utilizador é migrado e a migração deve ser transparente para os utilizadores. Para obter detalhes sobre a atribuição de objetos a um grupo do AAD, consulte o seguinte: 
- [Atribuir políticas](https://docs.microsoft.com/intune/get-started-policies) 
- [Atribuir perfis](https://docs.microsoft.com/intune/device-profile-assign) 
- [Atribuir aplicações](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Política de termos e condições
Assim como outras políticas ao nível do inquilino, políticas de termos e condições são migradas automaticamente para o Intune quando a autoridade mista estiver ativada para o seu inquilino.  No entanto, tem de atribuir os termos e condições para um grupo que contenha migrados que os utilizadores com precisão o relatório de aceitação para os utilizadores migrados e certifique-se de que os termos e condições corretamente são direcionadas para termos futuros e atualizações de condições ou dispositivo inscrições. Não é necessário que os utilizadores voltem a aceitar os termos e condições, a menos que existem alterações feitas à política na consola do Configuration Manager. Para obter detalhes, consulte [atribuir termos e condições](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configurar o conector do Exchange
Se utilizar o Exchange e tiver um conector do Exchange no local no Configuration Manager, terá [configurar o conector do Exchange no local no Intune](https://docs.microsoft.com/intune/exchange-connector-install). Considere também as informações nas secções seguintes para ajudar a migrar para o Exchange Connector do Intune e garantir o trabalho de acesso condicional corretamente após a migração.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Scripts do PowerShell para o ajudar a migrar para o Exchange Connector do Intune 
Scripts do PowerShell estão disponíveis para o ajudar a preparar para fazer a transição de seus dispositivos de Exchange a partir do Configuration Manager Exchange Connector para o Exchange Connector do Intune. Ao executar estes scripts estão opcionais, que recomendamos que executá-los para remover dispositivos Inativos do Exchange, o que impede que o Intune detetar dispositivos de desnecessários. Executar os scripts Certifique-se de que os dispositivos detetados através do Exchange podem intercalar com dispositivos inscritos no Intune, o mais tranqüila possível. Execute estes scripts antes de configurar o Intune Exchange Connector. Os scripts do PowerShell fazem parte da instalação importador de dados do Intune que utilizar para [importar dados do Configuration Manager para o Microsoft Intune](migrate-import-data.md) no próximo artigo. Para obter detalhes e para transferir os scripts, aceda a [importador de dados do Microsoft Intune](https://github.com/ConfigMgrTools/Intune-Data-Importer) página do GitHub.

### <a name="steps-to-ensure-conditional-access-works-properly-after-user-migration"></a>Passos para assegurar o acesso condicional funciona corretamente após a migração de utilizador
Para obter acesso condicional para funcionar corretamente depois de migrar utilizadores e para garantir que os utilizadores continuam a ter acesso ao respetivo servidor de e-mail, certifique-se de que a seguir for verdadeira:
- Se o Exchange ActiveSync acesso nível predefinição (da organização) é definida como bloqueio ou quarentena, dispositivos poderão perder o acesso ao e-mail. 
- Se o conector do Exchange estiver instalado no Configuration Manager e o **quando um dispositivo móvel não é gerido por uma regra de nível de acesso** definição tem um valor de **permitir o acesso**, tem de instalar o [ Conector do Exchange no local](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) no Intune antes de migrar os utilizadores. Configurar a definição de nível de acesso predefinida no Intune no **Exchange no local** painel no **definições de acesso do Advanced Exchange ActiveSync**. Para obter detalhes, consulte [configurar o Exchange no local acesso](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Utilize a mesma configuração para os dois conectores. O conector do último que configurar substitui as definições de organização do ActiveSync já gravadas pelo conector do outro. Se configurar os conectores de forma diferente, pode resultar em alterações de acesso condicional inesperado.
- Remova utilizadores de acesso condicional direcionamento no Configuration Manager, uma vez que eles são migrados para o Intune autónomo.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configurar o Microsoft Intune Certificate Connector
Se usar o NDES para emitir certificados através de SCEP, tem de configurar o Microsoft Intune Certificate Connector. O computador que aloja o conector do NDES no Intune não pode ser o mesmo computador que aloja o conector do NDES no Configuration Manager. Para obter detalhes, consulte [configurar e gerir certificados SCEP com o Intune](https://docs.microsoft.com/intune/certificates-scep-configure). 

> [!Important]    
> Depois de configurar o conector, tem de modificar importados perfis SCEP para referenciar o novo URL do servidor.

## <a name="next-step"></a>Passo seguinte
Depois de preparar o Intune para a migração, está pronto para migrar um conjunto de utilizadores de teste para o Intune autónomo. Para obter detalhes, consulte [alterar a autoridade MDM para utilizadores específicos (autoridade misturadas)](migrate-mixed-authority.md).


