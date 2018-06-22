---
title: Resolver problemas do SCAP
titleSuffix: Configuraton Manager
description: Importar as definições de compatibilidade SCAP como linhas de base de configuração e exportar os resultados
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 05010d73916ac4c012c157a470ed98dce47fc747
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334485"
---
# <a name="troubleshoot-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Resolver problemas relacionados com as extensões SCAP para o Microsoft System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão de pré-visualização técnica 1803 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Esta versão de pré-lançamento das extensões SCAP pode ser instalado em quaisquer versões atualmente suportadas do ramo atual do Configuration Manager e LTSB 1606. O ficheiro de instalação está localizado em cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir de pré-visualização técnica 1803. 

As extensões SCAP para o Microsoft System Center Configuration Manager foram concebidas para funcionar com os fluxos de dados SCAP que se destina a ferramenta SCAP validado com capacidade ACS para suportar USGCB. Normalmente, não será problemas com estes fluxos de dados USGCB SCAP que são transferidos do site do NIST.

No entanto, pode diagnosticar e resolver problemas que poderá ver utilizando os seguintes métodos:

- Certifique-se de que os componentes de cliente (scmdcm.msi) das extensões SCAP estão instalados em todos os computadores de destino.
- Reveja o resultado do ficheiro de registo da ferramenta Microsoft.Sces.ScapToDcm.exe.
- Reveja os problemas e soluções comuns quando utilizar as extensões SCAP.
- Contacte a Microsoft para questões ou comentários sobre as extensões SCAP.



## <a name="review-microsoftscesscaptodcmexe-tool-log"></a>Reveja o registo da ferramenta de Microsoft.Sces.ScapToDcm.exe

A ferramenta de Microsoft.Sces.ScapToDcm.exe cria um registo de nome personalizado quando o ficheiro – registo parâmetro for especificado. O ficheiro de registo tem informações sobre os resultados da execução da ferramenta de Microsoft.Sces.ScapToDcm.exe. Por exemplo, o ficheiro de registo tem o número de itens no ficheiro de entrada XCCDF/DataStream que foram removidos ou ignorados ao executar a ferramenta de Microsoft.Sces.ScapToDcm.exe.

A tabela seguinte lista algumas das informações que aparece no ficheiro de registo e uma descrição de cada tipo de informações.

### <a name="description-of-information-found-in-microsoftscesscaptodcmexe-log-files"></a>Descrição das informações encontradas nos ficheiros de registo Microsoft.Sces.ScapToDcm.exe

| Informações | Descrição |
| --- | --- |
| remover | Um item pode ser removido porque o tipo de teste não é um tipo de teste suportado. |
| Ignorar |O ID de definição OVAL destina-se uma plataforma inválida. </br> </br> O ID de definição OVAL não é referido pelo ficheiro de entrada XCCDF/DataStream.</br> </br> O ID de teste OVAL não é referido pelo ficheiro de entrada XCCDF/DataStream. </br> </br> O ID de perfil XCCDF não contém quaisquer @select instruções igual a 1. </br> </br> O ID de perfil XCCDF inclui um atributo abstrato que é verdadeiro. </br> </br> O ID de perfil XCCDF não contém uma regra Qualificável.|

## <a name="common-problems-and-solutions"></a>Problemas e soluções comuns

A tabela seguinte lista alguns problemas comuns e soluções para ajudar a resolver problemas.

Tabela 1.6 problemas e soluções comuns

| Problema | Solução possível |
| --- | --- |
| Se vir um **erro** ou **desconhecido** Estados de uma linha de base e o IE não conseguir mostram o relatório. O IE diz: &quot;o relatório está vazio ou é inválido&quot; | Selecione a linha de base e clique em **Evaluate** volte a executar a linha de base, em seguida, aguarde para monitorizar o **estado de compatibilidade**/**atualização da última avaliação**. Após a data da última avaliação é atualizada para a data/hora atuais (significa que a avaliação foi concluída), selecione a linha de base e veja o relatório novamente. Se o IE ainda não é possível ver o relatório, tal pode significar que a linha de base é demasiado grande. Voltar a gerar o conteúdo utilizando um tamanho de lote menor para criar linhas de base subordinadas mais pequenas. Se este problema ocorre em linhas de base principais, tente implementar linhas de base subordinadas em vez disso. |
| Posso ter criado objetos de política de grupo (GPOs) que incluem as definições USGCB prescritas e ligado-los para unidades organizacionais (UOs) que contêm computadores com Windows 7, mas os relatórios de compatibilidade indicam que algumas das definições não estão configuradas corretamente. | É possível que as permissões de política de grupo estejam incorretas ou que não foram ligadas à UO correta. No entanto, é mais provável que as novas definições não tenham sido aplicadas ainda. Por predefinição, a política de grupo, nos computadores cliente que pertençam a um domínio do Active Directory, verifique a existência de atualizações à política de grupo a cada 90 minutos. Isto pode ser um motivo por que razão as definições não parecem ter sido aplicados, apesar de ter configurado as políticas corretamente. Outro fator de recordar é que muitas definições de computador exigem um reinício antes de poderem demorar efeito. Por exemplo, a definição denominada * * criptografia de sistema: Utilize algoritmos compatíveis com do FIPS para encriptação, hashing e iniciar, necessita de reiniciar o computador para que Windows possam utilizar os algoritmos de encriptação especificado. Pode ignorar o intervalo de atualização de política de grupo ao introduzir o seguinte comando numa linha de comandos com privilégios de administrador: gpupdate /force após o grupo de política de atualização estiver concluída, reinicie o computador para se certificar de que todas as definições entram em vigor. Para obter mais informações, consulte: [Uma descrição do utilitário de atualização de política do grupo de](http://support.microsoft.com/kb/298444), artigo 298444 da Base de dados de conhecimento. |
| Estou a ter problemas a fornecer a ligação de base de dados com as minhas informações organizacionais. | Para obter informações sobre como configurar as suas informações de ligação de base de dados, consulte o [instalar e configurar o SCAP](/sccm/compliance/plan-design/scap/install-configure-scap) artigo. 

## <a name="next-step"></a>Passo seguinte
> [!div class="nextstepaction"]
> [Instalar e configurar as Extensões do SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)