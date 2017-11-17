---
title: "Alterar a autoridade de MDM para utilizadores específicos (misturadas autoridade de MDM)"
titleSuffix: Configuration Manager
description: "Saiba como alterar a autoridade de MDM híbrida MDM ao Intune autónomo para alguns utilizadores."
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/14/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 31d1d84c225d041f644669f0d3279e6bcd3f75ba
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/17/2017
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Alterar a autoridade de MDM para utilizadores específicos (misturadas autoridade de MDM) 

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

Pode configurar uma autoridade MDM mista no mesmo inquilino selecionando alguns utilizadores para serem geridos no Intune e outros utilizadores para serem geridos pelo MDM (Intune integrado com o Configuration Manager) híbrido. Este tópico fornece informações sobre como iniciar a mover os utilizadores ao Intune autónomo e parte do princípio de que concluiu os seguintes passos:
- Utilizar a ferramenta de importação de dados para [importar objetos do Configuration Manager para o Intune](migrate-import-data.md) (opcional).
- [Preparar o Intune para a migração de utilizador](migrate-prepare-intune.md) para garantir que os utilizadores e os respetivos dispositivos continuam a ser geridos depois de serem migrados.

> [!Note]    
> Se decidir que pretende efetuar uma reposição completa do seu inquilino, o que removerá todas as políticas, aplicações e inscrições de dispositivos, contacte o suporte para obter assistência.

Utilizadores migrados e os respetivos dispositivos serão geridos no Intune e outros dispositivos continuarão a ser gerido no Configuration Manager. Irá começar com um grupo de teste pequeno de utilizadores para verificar que tudo está a funcionar conforme esperado. Em seguida, gradualmente irá migrar grupos adicionais de utilizadores até estar pronto para mudar a autoridade de MDM de inquilinos do Configuration Manager para o Intune autónomo. 

## <a name="things-to-know-before-you-migrate-users"></a>Coisas que deve saber antes de migrar os utilizadores
- Durante a migração faseada, quaisquer políticas MDM ou aplicações no Configuration Manager existente continuam a aplicar a dispositivo MDM híbrida.
- Os utilizadores são adicionados a um grupo AAD designar como o grupo de migração. Todos os dispositivos associados a utilizadores no grupo de migração são geridos no Intune.
- Se os dispositivos são adicionados ao grupo AAD, são ignoradas, a menos que estão num dispositivo sem um utilizador associado.
- Os utilizadores não num grupo AAD marcados automaticamente para migração herdam a autoridade de MDM de inquilinos (Configuration Manager).
- Quando migrar um utilizador para o Intune, os utilizadores e os dispositivos serão apresentados do Intune no portal do Azure após cerca de 15 minutos.  
- Quando migra os utilizadores ao Intune autónomo, continue a gerir as seguintes definições do Configuration Manager para o Intune autónomo e híbridos MDM dispositivos:
    - [Certificado do Apple Push Notification (APNs) do serviço](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)
    - [Programa de inscrição de dispositivos](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)
    - Perfis de inscrição
    - [Licenças do volume Purchase Program (VPP)](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)
    - Identificadores de empresa 
    - [Certificados de assinatura de código](/sccm/mdm/deploy-use/enroll-hybrid-windows)
    - [Categorias de dispositivos](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)
    - [Gestores de inscrição](/sccm/mdm/plan-design/device-enrollment-methods)
    - Termos e condições
    - Windows SLKs
    - Uma imagem corporativa do Portal de empresa    
      
> [!Important]    
  > Continue a editar as políticas ao nível do inquilino através da consola do Configuration Manager. Depois de [alterar a sua autoridade MDM de inquilinos](change-mdm-authority.md) ao Intune, em seguida, que irá gerir estas políticas no Intune no Azure. 
- Recomendamos que não migrar as contas de utilizador que foram adicionadas como gestores de inscrição de dispositivos no Configuration Manager. Mais tarde, quando alterar a autoridade de MDM de inquilinos para o Intune, estas contas de utilizador irão migrar corretamente. Se migrar conta do utilizador de Gestor de inscrição do dispositivo antes da alteração de autoridade MDM de inquilinos, tem de adicionar manualmente o utilizador como um Gestor de inscrição de dispositivos no Intune no Azure. No entanto, os dispositivos inscritos utilizando o Gestor de inscrição de dispositivos não são migrados com êxito. Tem de chamar o suporte para migrar estes dispositivos. Para obter mais informações, consulte [adicionar um Gestor de inscrição de dispositivos](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).
- Dispositivos inscritos utilizando o Gestor de inscrição de dispositivos e os dispositivos que não tem utilizadores associados não são migrados para a autoridade de MDM de novo. Para os dispositivos, tem de chamar o suporte para ajudá-lo com os dispositivos individuais. Não tem suporte executar uma reposição de autoridade MDM ou irá eliminar os dados no Intune. Tem [alterar a autoridade de MDM](migrate-change-mdm-authority.md) partir da consola do Configuration Manager.

## <a name="migrate-users-to-intune"></a>Migrar os utilizadores ao Intune
Para testar as configurações do Intune estão a funcionar conforme esperado, migre primeiro um pequeno conjunto de utilizadores e os respetivos dispositivos. Em seguida, depois de confirmar coisas estão a funcionar conforme esperado, pode começar a migrar mais AAD grupos com mais utilizadores e os respetivos dispositivos.

## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Migrar de um grupo de teste de utilizadores ao Intune autónomo
Podem inscrever os dispositivos para os utilizadores na coleção associada a subscrição do Intune híbrido MDM. Ao remover um utilizador da coleção, os dispositivos inscritos são migrados para o Intune autónomo, se o utilizador tiver atribuída uma licença do Intune. Se ainda não já atribuído licenças a utilizadores que planeia migrar, consulte [licenças do Intune atribuir às suas contas de utilizador](https://docs.microsoft.com/intune/licenses-assign). Na coleção para a subscrição do Intune, pode excluir coleções de utilizadores da sua coleção principal para migrar os utilizadores na coleção excluída. 

No exemplo seguinte, a coleção de utilizadores híbrida contém todos os membros da coleção de todos os utilizadores. Isto permite que qualquer utilizador inscrever um dispositivo para híbrida MDM. Para migrar os utilizadores ao Intune autónomo, selecione excluir coleções e adicionar uma coleção com os utilizadores a migrar. Quando estiver pronto para migrar mais utilizadores, pode adicionar as coleções excluídas adicionais que incluem esses utilizadores. 

![Excluir a coleções](../media/migrate-excludecollections.png)

> [!Note] 
> Se tiver o **todos os utilizadores** coleção selecionada para a subscrição do Intune, não tem permissão para adicionar uma regra para excluir a coleções. Criar uma nova coleção com base no **todos os utilizadores** coleção, certifique-se de que a coleção contém os utilizadores que espera e, em seguida, edite a subscrição do Intune para utilizar a nova coleção. Pode excluir coleções de utilizadores de nova coleção para migrar os utilizadores. 

Para migrar um grupo de teste de utilizadores ao Intune, crie uma coleção de utilizador que contêm os utilizadores para migrar e, em seguida, excluir a coleção de utilizadores de coleção utilizada para a subscrição do Intune.   

O diagrama seguinte fornece uma descrição geral de funcionamento da migração de utilizador.

 ![Descrição geral de misto de autoridade](../media/migrate-mixedauthority.svg)

1. Certifique-se de que o utilizador tem uma licença do Intune/EMS. 
2. Crie uma coleção para excluir da coleção para a subscrição do Intune. Neste exemplo, o **utilizadores híbrida todos os** coleção contém uma regra para excluir os utilizadores a **piloto de migração** coleção. **User1** é um membro do **piloto de migração** coleção e está excluído do **utilizadores híbrida todos os** coleção. 
3. **User1**do dispositivos são agora geridos do Intune no portal do Azure. 
4. Todos os outros dispositivos continuam a ser geridos a partir da consola do Configuration Manager. 

## <a name="verify-intune-standalone-functionality"></a>Verificar a funcionalidade do Intune autónomo
Depois de ter migrado um pequeno conjunto de utilizadores, certifique-se de que os dispositivos do utilizador estão listados no Intune. Vá para o **dispositivos** painel e selecione **todos os dispositivos**. 

Em seguida, certifique-se de que as políticas, perfis, aplicações, etc. estão a funcionar conforme esperado dos dispositivos dos utilizadores.

## <a name="migrate-additional-users"></a>Migrar utilizadores adicionais
Depois de ter verificado que autónoma do Intune está a funcionar como esperado, pode começar a migrar utilizadores adicionais. Tal como criar uma coleção com um conjunto de utilizadores de teste, crie coleções que contêm utilizadores e migrar excluir essas coleções na coleção associada a subscrição do Intune. Para obter mais informações, consulte [coleção associados a sua subscrição do Intune](#collection-associated-with-your-intune-subscription).

## <a name="next-steps"></a>Passos seguintes
Depois de ter migrado os utilizadores e testar a funcionalidade do Intune, considere se estiver pronto para [alterar a autoridade de MDM](migrate-change-mdm-authority.md) do seu inquilino do Intune do Configuration Manager para o Intune. 