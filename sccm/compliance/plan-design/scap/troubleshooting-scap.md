---
title: Resolver problemas relacionados com o SCAP
titleSuffix: Configuration Manager
description: Saiba como resolver problemas com as extensões SCAP para o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 58a3c69e6206aa651e55f96286f98f64f748de70
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137141"
---
# <a name="troubleshoot-the-scap-extensions-for-configuration-manager"></a>Resolver problemas relacionados com as extensões SCAP para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As extensões SCAP para o Configuration Manager foram concebidas para funcionar com os fluxos de dados SCAP pretendidos para a ferramenta SCAP validado com capacidade ACS para suportar USGCB. Normalmente, não tiver problemas com estes fluxos de dados USGCB SCAP que são transferidos a partir do site do NIST.

Diagnosticar e resolver problemas através dos seguintes métodos:  

- Certifique-se de que os componentes de cliente (scmdcm) de extensões do SCAP estão instalados em todos os computadores de destino.  

- Reveja o resultado do ficheiro de registo da ferramenta Microsoft.Sces.ScapToDcm.exe.  

- Rever problemas e soluções comuns quando utilizar as extensões SCAP.  

- Contacte a Microsoft para questões ou comentários sobre as extensões SCAP.



## <a name="review-microsoftscesscaptodcmexe-log"></a>Registo de Microsoft.Sces.ScapToDcm.exe de revisão

A ferramenta de Microsoft.Sces.ScapToDcm.exe cria um ficheiro de registo com nome personalizado quando especificar o `–log` parâmetro. O ficheiro de registo tem informações sobre os resultados da execução da ferramenta de Microsoft.Sces.ScapToDcm.exe. Por exemplo, incluem o número de itens no arquivo de entrada XCCDF/DataStream que foram removidos ou ignorados durante a execução da ferramenta de Microsoft.Sces.ScapToDcm.exe.

A tabela seguinte lista algumas das informações que é apresentado no ficheiro de registo e uma descrição de cada tipo de informações.

### <a name="information-found-in-the-microsoftscesscaptodcmexe-log-file"></a>Informações encontradas no arquivo de log Microsoft.Sces.ScapToDcm.exe

| Informações | Descrição |
| --- | --- |
| **Remover** | Um item pode ser removido porque o tipo de teste não é um tipo de testes com suporte. |
| **Ignorar** | O ID de definição OVAL destina-se uma plataforma inválida. </br> </br> O ID de definição OVAL não é referido pelo ficheiro de entrada XCCDF/DataStream.</br> </br> O ID de teste OVAL não é referido pelo ficheiro de entrada XCCDF/DataStream. </br> </br> O ID de perfil XCCDF não contém nenhum `@select` instruções igual a 1. </br> </br> O ID de perfil XCCDF inclui um atributo abstrato que é verdadeiro. </br> </br> O ID de perfil XCCDF não contém uma regra Qualificável.|



## <a name="common-problems-and-solutions"></a>Problemas e soluções comuns

Seguem-se alguns problemas e soluções para ajudar a resolver problemas comuns.

- Verá uma **erro** ou **desconhecido** estado para uma linha de base e o Internet Explorer não conseguir mostra o relatório. O erro do navegador é, "o relatório está vazio ou é inválido."  

     - Execute novamente a linha de base. Selecione a linha de base e clique em **Evaluate**. Em seguida, aguarde para monitorizar o **estado de compatibilidade**/**atualização da última avaliação**. Após a data da última avaliação é atualizada para a data/hora atual, que significa que a avaliação foi concluída, selecione a linha de base e veja o relatório novamente.  

     - Se o Internet Explorer ainda não é possível ver o relatório, pode significar que a linha de base é demasiado grande. Voltar a gerar o conteúdo utilizando um tamanho de lote menor para criar linhas de base subordinadas mais pequenas.  

     - Se este problema ocorre em linhas de base principais, tente implementar linhas de base subordinadas em vez disso.  

- Criei objetos de política de grupo (GPOs) que incluem as definições USGCB prescritas. Eu liguei-as unidades organizacionais (UOs) que contêm os computadores que executam o Windows 7. Os relatórios de conformidade indicam que algumas das definições não estão configuradas corretamente.  

     - É possível que as permissões de política de grupo estão incorretas ou ainda não foi anexados à UO correta.  

     - É mais provável que as novas definições ainda ainda não foram aplicadas. Por predefinição, clientes do Active Directory procurar atualizações à política de grupo a cada 90 minutos. Esse ciclo pode ser um dos motivos por que as definições não são apresentados para terem sido aplicadas, mesmo que configurou corretamente as políticas.  

     - Muitas configurações de computador requerem um reinício antes que só são aplicadas. Por exemplo, a definição de **criptografia de sistema: Utilizar algoritmos compatíveis com FIPS para encriptação, hash e assinatura** , tem de reiniciar o computador para o Windows consiga utilizar os algoritmos de encriptação especificados. Ignorar o intervalo de atualização de política de grupo introduzindo o seguinte comando no prompt de comando com privilégios de administrador: `gpupdate /force`. Depois de concluída a atualização da política de grupo, reinicie o computador para se certificar de que todas as definições entrem em vigor. Para obter mais informações, consulte [uma descrição do utilitário de atualização de política de grupo](https://support.microsoft.com/help/298444).

- Estou a ter problemas a fornecer a ligação de base de dados com minhas informações organizacionais.  

     - Para obter mais informações sobre como configurar a ligação de base de dados, consulte [instalar e configurar o SCAP](/sccm/compliance/plan-design/scap/install-configure-scap).  
