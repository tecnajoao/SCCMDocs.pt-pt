---
title: Mensagens de erro
titleSuffix: Configuration Manager
description: Saiba mais sobre as mensagens de erro do Gestor de conversão de pacotes.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 62c4453cc383fa14eebf6e66c2582b878aaebae2
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297762"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Referência técnica para mensagens de erro do Gestor de conversão de pacotes

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1357861-->

Este artigo descreve as mensagens de erro que exibe o Gestor de conversão de pacotes. Ele também inclui as possíveis causas do erro e métodos para corrigir o erro. Gestor de conversão de pacotes regista mensagens de erro nos **PCMTrace.log**. Para obter mais informações, incluindo como controlar o nível de verbosidade, consulte [ficheiros de registo](/sccm/apps/pcm/troubleshoot-pcm#log-files).


#### <a name="application-creation-failed-with-the-following-exception"></a>Falha na criação de aplicativos com a exceção seguinte

A exceção especificada ocorreu durante a submissão do objeto aplicacional ao servidor do Configuration Manager.

Verifique as suas permissões no Configuration Manager, valide a sua conectividade e tente novamente. Se essas ações não corrigir o problema, examine o **PCMtrace.log** ficheiro (nível de verbosidade 4) e **smsprov. log**.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Erro de conversão – aplica-se para um Estado de transformação do pacote

Ocorreu uma exceção geral durante a conversão do pacote. Consulte a **PCMtrace.log** ficheiro (nível de verbosidade 4).

Verifique as permissões de utilizador para a partilha de rede (origem de dados de pacote), valide a sua conectividade e tente novamente. Se essas ações não corrigir o problema, examine o **PCMtrace.log** ficheiro (nível de verbosidade 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>Não foi encontrado um pacote convertido e a sua aplicação resultante do mesmo nas saídas de fluxo de trabalho
A aplicação (programa/pacote convertido) foi eliminada.

Modifique o programa/pacote dependente para garantir que o programa/pacote dependente existe.


#### <a name="objects-were-not-created-successfully"></a>Objetos não foram criados com êxito
Existem várias causas possíveis.

Verifique as suas permissões no Configuration Manager, valide a sua conectividade e tente novamente. Se essas ações não corrigir o problema, examine o **PCMtrace.log** ficheiro (nível de verbosidade 4) e o **smsprov. log** ficheiro.


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Feche o assistente e resolva quaisquer problemas com o pacote selecionado. Consulte PCMTrace.Log para obter mais detalhes
Existem várias causas possíveis.

Verifique as suas permissões no Configuration Manager, valide a sua conectividade e tente novamente. Se essas ações não corrigir o problema, examine o **PCMtrace.log** ficheiro (nível de verbosidade 4) e o **smsprov. log** ficheiro.


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>Alguns tipos de implementação faltam métodos de deteção. Todos os tipos de implementação tem de ter métodos de deteção
Faltam métodos de deteção do programa.

Adicione um ou mais métodos de deteção durante o **corrigir e converter** processo.


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Ocorreu um erro ao preparar o pacote para conversão
Existem várias causas possíveis.

Verifique as suas permissões no Configuration Manager, valide a sua conectividade e tente novamente. Se essas ações não corrigir o problema, examine o **PCMtrace.log** ficheiro (nível de verbosidade 4) e o **smsprov. log** ficheiro.


