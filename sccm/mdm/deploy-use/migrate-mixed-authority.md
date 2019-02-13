---
title: Alterar a autoridade MDM
titleSuffix: Configuration Manager
description: Saiba como alterar a autoridade de MDM da MDM híbrida para o Intune autónomo para utilizadores específicos (autoridade de MDM mista).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7ede0049847eda2b87731f4cfbce0bda8984f158
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120253"
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Alterar a autoridade MDM para utilizadores específicos (autoridade MDM mista) 

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

Pode configurar uma autoridade MDM mista no mesmo inquilino. Gerir alguns utilizadores do Microsoft Intune e outros híbrido MDM. Este artigo fornece informações sobre como começar a mover os utilizadores para o Intune autónomo. Parte do princípio de que concluiu os seguintes passos:  

- Usei a ferramenta de importação de dados para [importar objetos do Configuration Manager para o Intune](migrate-import-data.md) (opcional).  

- [Preparar o Intune para a migração de utilizador](migrate-prepare-intune.md) para se certificar de que os utilizadores e os respetivos dispositivos continuam a ser geridos depois de serem migradas.  

> [!Note]    
> Uma reposição completa do seu inquilino remove todas as políticas, aplicações e inscrições de dispositivos. Se decidir que pretende fazer esse processo, contacte o suporte para obter assistência.  

Gerir utilizadores migrados e os respetivos dispositivos no Intune. Continue a gerir outros dispositivos no Configuration Manager. Para verificar se tudo o que está a funcionar conforme esperado, comece com um pequeno grupo de teste de utilizadores. Em seguida, migre gradualmente grupos de utilizadores adicionais. Quando estiver pronto, mude a autoridade de MDM do Configuration Manager de nível de inquilino para o Intune autónomo. 

> [!Important]  
> A partir de 13 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="things-to-know-before-you-migrate-users"></a>Que precisa saber antes de migrar utilizadores

- Durante a migração faseada, quaisquer políticas MDM existente ou a aplicações no Configuration Manager continuam a aplicar a dispositivos MDM híbrida.  

- Os dispositivos para os utilizadores na coleção associada com a subscrição do Intune podem inscrever-se no hybrid MDM. Todos os dispositivos associados a utilizadores não na coleção são geridos no Intune, desde que o utilizador tem uma licença do Intune/EMS.   

    > [!Note]  
    > Os utilizadores podem inscrever no Intune autónomo, mesmo se tiver bloqueado-los através da consola do Configuration Manager. Para impedir completamente um utilizador a inscrição, não licenças os utilizadores indesejados para o Intune. Eles não podem inscrever-se sem uma licença.<!--SCCMDocs issue 738-->  

- Quando migra um utilizador ao Intune, o utilizador e os dispositivos são apresentados no Intune no portal do Azure depois de cerca de 15 minutos.   

- Ao migrar utilizadores para o Intune autónomo, continue a gerir as seguintes definições do Configuration Manager para ambos os dispositivos MDM do Intune autónomo e híbrido:  

    - [Certificado Apple Push Notification service (APNs)](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)  

    - [Programa de inscrição de dispositivos](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)  

        > [!Note]  
        > Não precisa de recriar o token do DEP ou removê-lo do Configuration Manager. Ele migra automaticamente para o Intune 24 horas depois de o alterar autoridade de MDM do inquilino no Configuration Manager para o Intune. Esta alteração é a etapa final na migração. (Se o token do DEP não migrar dentro de 24 horas, contacte o suporte da Microsoft para obter assistência.)  

    - Perfis de inscrição  

    - [Licenças do volume Purchase Program (VPP)](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)  

    - Identificadores empresariais  

    - [Certificados de assinatura de código](/sccm/mdm/deploy-use/enroll-hybrid-windows)  

    - [Categorias de dispositivos](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)  

    - [Gestores de inscrição](/sccm/mdm/plan-design/device-enrollment-methods)  

    - Termos e condições  

    - SLKs do Windows  

    - Imagem corporativa de Portal da empresa    

      
  > [!Important]    
  > Continue a editar as políticas ao nível do inquilino, utilizando a consola do Configuration Manager. Depois de [alterar a autoridade MDM de inquilinos](/sccm/mdm/deploy-use/change-mdm-authority) ao Intune, as políticas ao nível do inquilino que foram a gerir no Configuration Manager automaticamente migrar para o Intune no Azure. É um exemplo destas políticas de certificados do Apple Push Notification service (APNs).<!--SCCMDocs issue #971-->  

-   Se utilizar certificados de assinatura de código, recomendamos que migrar utilizadores numa abordagem faseada. Após a migração de um dispositivo móvel, faz um pedido de autoridade de certificado para um novo certificado. Ao utilizar uma abordagem faseada para migrar os utilizadores (e os respetivos dispositivos), ele limita o número de pedidos de autoridade de certificação simultâneas.  

- Não migre as contas de utilizador que foram adicionadas como gestores de inscrição de dispositivos (DEM) no Configuration Manager. Mais tarde, quando mudar a autoridade MDM de inquilinos para o Intune, estas contas de utilizador migrar corretamente. Se migrar a conta de utilizador DEM antes da alteração de autoridade MDM de nível de inquilino, tem de adicionar manualmente o utilizador como um DEM no Intune no Azure. No entanto, os dispositivos inscritos através de um DEM não migrar com êxito. Contacte o suporte para migrar estes dispositivos. Para obter mais informações, consulte [adicionar um Gestor de inscrição de dispositivos](https://docs.microsoft.com/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).  

    > [!Note]  
    > No modo misto autoridade, não mova estas contas para o Intune, removendo-os partir da coleção de nuvem do ConfigMgr. Se o fizer, o usuário torna-se um usuário padrão e não é possível inscrever mais de 15 dispositivos. Migre em vez disso, estes utilizadores e os respetivos dispositivos depois de mudar completamente a autoridade de MDM para o inquilino.<!--Intune bug 2174210-->  

- Dispositivos inscritos com um DEM e dispositivos sem [afinidade de utilizador](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) não são migradas automaticamente para a nova autoridade MDM. Para mudar a autoridade de gestão para estes dispositivos MDM, veja [migrar dispositivos sem afinidade do utilizador](#migrate-devices-without-user-affinity).  



## <a name="migrate-users-to-intune"></a>Migrar utilizadores para o Intune

Para testar as configurações do Intune estão a funcionar conforme esperado, migre pela primeira vez um pequeno conjunto de utilizadores e os respetivos dispositivos. Em seguida, depois de confirmar as coisas estão funcionando como esperado, pode começar a migrar mais grupos do AAD com mais usuários e os respetivos dispositivos.



## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Migrar um grupo de teste de utilizadores para o Intune autónomo

Os dispositivos para os utilizadores na coleção associada com a subscrição do Intune podem inscrever-se no hybrid MDM. Quando remover um utilizador da coleção, se o utilizador tiver uma licença do Intune atribuída, os seus dispositivos inscritos são migrados para o Intune autónomo. Se ainda não já atribuiu licenças aos utilizadores que pretende migrar, consulte [atribuir licenças do Intune às contas de utilizador](https://docs.microsoft.com/intune/licenses-assign). Na coleção para a subscrição do Intune, pode excluir coleções de utilizadores da sua coleção principal para migrar os utilizadores na coleção excluída. 

No exemplo seguinte, a coleção de utilizadores híbrida contém todos os membros da coleção de todos os utilizadores. Esta configuração permite que qualquer utilizador inscreve um dispositivo para hybrid MDM. Para migrar utilizadores para o Intune autónomo, selecione excluir coleções e adicionar uma coleção com os utilizadores a migração. Quando estiver pronto para migrar mais usuários, adicione as coleções excluídas adicionais que incluem esses utilizadores. 

![Excluir coleções](../media/migrate-excludecollections.png)

> [!Note]  
> Quando tem o **todos os utilizadores** coleção selecionada para a subscrição do Intune, não tem permissão para adicionar uma regra para excluir coleções. Criar uma nova coleção com base na **todos os utilizadores** coleção. Certifique-se de que a coleção contém os utilizadores que pretende. Em seguida, edite a subscrição do Intune para utilizar a nova coleção. Pode excluir coleções de utilizadores da nova coleção para migrar os utilizadores.  

Para migrar um grupo de teste de utilizadores ao Intune, crie uma coleção de utilizadores que contenha os utilizadores a migrar. Em seguida, exclua a coleção de utilizador da coleção que é utilizada para a subscrição do Intune.   

O diagrama seguinte fornece uma descrição geral de como funciona a migração do usuário.

 ![Descrição geral de autoridade misto](../media/migrate-mixedauthority.svg)

1. Certifique-se de que o utilizador tem uma licença do Intune/EMS.   

2. Crie uma coleção para excluir da coleção para a subscrição do Intune. Neste exemplo, o **os usuários de todos os híbrida** coleção contém uma regra para excluir usuários no **piloto de migração** coleção. **Utilizador1** é um membro do **piloto de migração** coleção e é excluído do **utilizadores híbrida todos os** coleção.  

3. **Utilizador1**do dispositivos são agora geridos do Intune no portal do Azure.   

4. Todos os outros dispositivos continuam a ser geridas na consola do Configuration Manager.  



## <a name="verify-intune-standalone-functionality"></a>Verificar a funcionalidade do Intune autónomo

Depois de migrar um pequeno conjunto de utilizadores, certifique-se de que os dispositivos do utilizador estão listados no Intune. Aceda a **dispositivos**e selecione **todos os dispositivos**. 

Em seguida, certifique-se de que as políticas, perfis e aplicações estão a funcionar conforme esperado nos dispositivos de utilizador.



## <a name="migrate-additional-users"></a>Migrar utilizadores adicionais

Depois de verificar que o Intune autónomo esteja funcionando como esperado, comece a migrar os utilizadores adicionais. Tal como uma coleção que criou com um conjunto de utilizadores de teste, crie coleções que incluem os utilizadores a migração. Exclua essas coleções da coleção que está associada a subscrição do Intune. Para obter detalhes, consulte [coleção associados a sua subscrição do Intune](#collection-associated-with-your-intune-subscription).



## <a name="migrate-devices-without-user-affinity"></a>Migrar dispositivos sem afinidade do utilizador

Dispositivos inscritos através do Gestor de inscrição de dispositivos e dispositivos sem [afinidade de utilizador](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) não são migradas automaticamente para a nova autoridade MDM. Pode utilizar o *comutador MdmDeviceAuthority* cmdlet do PowerShell para alternar entre o Intune e Configuration Manager autoridades de gestão nos seguintes cenários: 

-   Cenário 1: Utilize o *comutador MdmDeviceAuthority* cmdlet para migrar dispositivos selecionados e validar que podem ser geridos com o Intune no Azure. Em seguida, quando estiver pronto, [alterar a autoridade de MDM para o Intune para o inquilino](migrate-change-mdm-authority.md) para concluir a migração para os dispositivos.  

-   Cenário 2: Quando estiver pronto para alterar a autoridade de MDM para o Intune para o inquilino, execute as ações seguintes para migrar os seus dispositivos sem afinidade do utilizador:  

    - Utilize o cmdlet para alterar a autoridade MDM para os seus dispositivos sem afinidade do utilizador antes de [alterar a autoridade de MDM para o Intune para o inquilino](migrate-change-mdm-authority.md).     

    - Contacte o suporte para que os dispositivos sem afinidade do utilizador switched depois de alterar a autoridade de MDM para o Intune para o inquilino.  

Para mudar a autoridade de gestão para estes dispositivos MDM, pode utilizar o *comutador MdmDeviceAuthority* cmdlet para alternar entre autoridades de gestão do Intune e Configuration Manager. 

### <a name="cmdlet-switch-mdmdeviceauthority"></a>Cmdlet *MdmDeviceAuthority de comutador*

#### <a name="synopsis"></a>SYNOPSIS
O cmdlet muda a autoridade de gestão de dispositivos do MDM sem afinidade do utilizador (por exemplo, dispositivos inscritos em massa). O cmdlet alterna entre o Intune e Configuration Manager autoridades de gestão. Ele muda para os dispositivos especificados com base na respetivas autoridades de gestão quando executar o cmdlet.

### <a name="syntax"></a>SINTAXE
`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>PARÂMETROS
#### `-Credential <PSCredential>`
Um objeto de credencial do PowerShell para a conta de utilizador do Azure AD que é utilizada quando a troca de autoridades de gestão do dispositivo. Se o parâmetro não for especificado, é pedido ao utilizador as credenciais. A função de diretório para esta conta de utilizador deve ser um **Administrador Global** ou uma **administrador limitado** com a função de administrador do **administrador do Intune**.

#### `-DeviceIds <Guid[]>`
Os IDs dos dispositivos MDM que tem de ter a sua autoridade de gestão mudada. O dispositivo IDs são identificadores exclusivos para os dispositivos apresentados pela consola do Configuration Manager.

#### `-Force [<SwitchParameter>]`
Especifica um parâmetro para desabilitar o prompt deve continuar.<br>
 
#### `-LogFilePath <string>`
Caminho para a localização do ficheiro de registo.
 
#### `-LoggingLevel <SourceLevels>`
O registo de nível usado para determinar o tipo de registos que precisam de ser escrito para o ficheiro de registo.
 
Seguem-se os valores possíveis para LoggingLevel:

  - ActivityTracing
  - Todas
  - Crítico
  - Erro
  - Informações
  - Desativado
  - Verboso
  - Aviso
 
#### `-Confirm [<SwitchParameter>]`
Pede-lhe confirmação antes de executar o comando.
 
#### `-WhatIf [<SwitchParameter>]`
Descreve o que aconteceria se tiver executado o comando sem realmente executar o comando.
 
#### `<CommonParameters>`
Este cmdlet suporta os parâmetros comuns: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer, PipelineVariable e OutVariable. Para obter mais informações, consulte [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

### <a name="example-1"></a>Exemplo 1

``` powershell
C:\PS>Switch-MdmDeviceAuthority -Credential $creds -DeviceIds $deviceIds
 
  DeviceId       : 62e6ea43-18f8-4278-bcd4-a4baed2c6d24
  Success        : True
  FailureReason  :
  NewAuthority   : Intune
  CompletionTime : 11/15/2017 8:00:11 PM
 
Description
 
-----------
 
Successfully switched the management authority of the device from Configuration Manager to Intune.
```

### <a name="remarks"></a>COMENTÁRIOS
- Para ver os exemplos, escreva: `get-help Switch-MdmDeviceAuthority -examples`  
- Para obter mais informações, escreva: `get-help Switch-MdmDeviceAuthority -detailed`  
- Para obter informações técnicas, escreva: `get-help Switch-MdmDeviceAuthority -full`  
- Para obter ajuda online, escreva: `get-help Switch-MdmDeviceAuthority -online`   



## <a name="next-steps"></a>Passos seguintes

Depois de migrar utilizadores e testar a funcionalidade do Intune, considere se está pronto para [alterar a autoridade MDM](migrate-change-mdm-authority.md) do seu inquilino do Intune do Configuration Manager para o Intune. 
