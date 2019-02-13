---
title: Monitorizar perfis de certificado
titleSuffix: Configuration Manager
description: Saiba como monitorizar o estado de compatibilidade dos perfis de certificado do System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 86485a1a54acb122e1b56118de9e72d840e01809
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137665"
---
# <a name="how-to-monitor-certificate-profiles-in-system-center-configuration-manager"></a>Como monitorizar perfis de certificado no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Ver resultados de compatibilidade na consola do Configuration Manager  

Para monitorizar a conformidade de certificado SCEP não utilize a consola, em vez disso, utilize [relatórios](#view-compliance-results-by-using-reports). 

1. Na consola do Configuration Manager, escolha **monitorização**>  **implementações**.  

2. Selecione a implementação de perfil de certificado de interesse.  

3. Rever as informações de conformidade de certificado resumo na página principal. Para obter informações mais detalhadas, selecione o perfil de certificado e, em seguida, no **home page** separador a **implantação** de grupo, escolha **ver o estado** para abrir o  **Estado da implementação** página.  

    A página **Estado da Implementação** contém os seguintes separadores:  

   -   **Em conformidade**: Apresenta a compatibilidade do perfil de certificado com base no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário no nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** . Este nó contém todos os utilizadores que são compatíveis com o perfil de certificado. O painel **Detalhes de Ativos** também apresenta os utilizadores que estão em conformidade com este perfil. Faça duplo clique num utilizador da lista para obter mais informações.  

       > [!IMPORTANT]  
       >  Um perfil de certificado não é avaliado se não for aplicável num dispositivo cliente. No entanto, é devolvido como compatível.  

   -   **Erro**: Apresenta uma lista de todos os erros para a implementação de perfil de certificado selecionado com base no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário no nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** . Este nó contém todos os utilizadores que geraram erros com este perfil. Quando selecionar um utilizador, o painel **Detalhes do Ativo** apresenta os utilizadores que são afetados pelo problema selecionado. Faça duplo clique num utilizador na lista para visualizar para obter mais informações.  

   -   **Não compatível**: Mostra uma lista de todas as regras não compatíveis no perfil de certificado com base no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário no nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** . Este nó contém todos os utilizadores que não são compatíveis com este perfil. Quando selecionar um utilizador, o painel **Detalhes do Ativo** apresenta os utilizadores que são afetados pelo problema selecionado. Faça duplo clique num utilizador da lista para visualizar mais informações sobre o problema.  

   -   **Desconhecido**: Apresenta uma lista de todos os utilizadores que não comunicaram compatibilidade para a implementação de perfil de certificado selecionado, juntamente com o estado atual do cliente dos dispositivos.  

4. Sobre o **estado de implementação** , reveja as informações detalhadas sobre a compatibilidade do perfil de certificado implementado. É criado um nó temporário no nó **Implementações** que o ajuda a localizar novamente estas informações de forma rápida.  

    O estado de inscrição do certificado é apresentado como um número. Utilize a tabela a seguir para compreender o que cada número significa:  


   | Estado de inscrição |                                                                                                                   Descrição                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         A inscrição foi efetuada com êxito e o certificado foi emitido.                                                                                          |
   |    0x00000002     |                                                                    O pedido foi apresentado e o registo está pendente ou o pedido foi emitido fora da banda.                                                                    |
   |    0x00000004     |                                                                                                          A inscrição tem de ser adiada.                                                                                                           |
   |    0x00000010     |                                                                                                               Ocorreu um erro.                                                                                                                |
   |    0x00000020     |                                                                                                        O estado de inscrição é desconhecido.                                                                                                        |
   |    0x00000040     | As informações de estado foram ignoradas. Isto pode ocorrer se um HIPERLINK "<http://msdn.microsoft.com/windows/ms721572>" autoridade de certificação \l security_certification_authority_gly"não é válida ou não tiver sido selecionada para a monitorização. |
   |    0x00000100     |                                                                                                           A inscrição foi negada.                                                                                                           |

##  <a name="view-compliance-results-by-using-reports"></a>Ver resultados de compatibilidade através de relatórios

 Definições de compatibilidade no System Center Configuration Manager incluem relatórios incorporados que pode utilizar para monitorizar informações sobre perfis de certificado. Estes relatórios têm a categoria de relatório de **Gestão de Compatibilidade e Definições**.  

> [!IMPORTANT]  
>  Deverá utilizar um caráter universal (%) ao utilizar os parâmetros **Filtro do dispositivo** e **Filtro do utilizador** nos relatórios de definições de compatibilidade.  

Para monitorizar a conformidade de certificado SCEP Utilize estes relatórios de certificado no nó de relatório **acesso a recursos da empresa**:  

 -   Histórico de emissão de certificados  
 -   Lista de recursos com certificados prestes a expirar  
 -   Lista de recursos por estado de emissão de certificados  



 Para obter mais informações sobre como configurar os relatórios no System Center Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  
