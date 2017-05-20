---
title: "A ferramenta de limpeza da biblioteca de conteúdos | Documentos do Microsoft"
description: "Utilize a ferramenta de limpeza da biblioteca de conteúdos para remover conteúdo órfão já não é associado a uma implementação do System Center Configuration Manager."
ms.custom: na
ms.date: 4/7/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 32f7fc4ef9c8e8d3c2ec8eeaf9a3174bad992ffb
ms.openlocfilehash: 76e6772bdd5cbd32d525e728f6ebc988b045da78
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="the-content-library-cleanup-tool-for-system-center-configuration-manager"></a>A ferramenta de limpeza de biblioteca de conteúdos para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 A partir da versão 1702, pode utilizar uma ferramenta de linha de comandos (**ContentLibraryCleanup.exe**) remover o conteúdo que é mais longa não associados a qualquer pacote ou aplicação a partir de um ponto de distribuição (órfãos conteúdo). Esta ferramenta chama-se a ferramenta de limpeza da biblioteca de conteúdos e substitui versões mais antigas do ferramentas semelhantes lançadas para produtos anteriores do Configuration Manager.  

A ferramenta afeta apenas o conteúdo no ponto de distribuição que especificou quando executa a ferramenta. A ferramenta não é possível remover o conteúdo da biblioteca de conteúdos no servidor do site.

Pode encontrar **ContentLibraryCleanup.exe** no *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* pasta no servidor do site num site de administração central ou site primário.

## <a name="requirements"></a>Requisitos  
 A ferramenta apenas pode ser executadas em relação a um único ponto de distribuição cada vez.  
 - -Pode executar diretamente no computador que aloja o ponto de distribuição que pretende limpar ou remotamente a partir de outro servidor.
 - A conta de utilizador que executa a ferramenta tem de ter permissões de administração baseada em funções direta iguais a um administrador total na hierarquia do Configuration Manager. A ferramenta não funciona quando a conta recebe estas permissões como membro de um grupo de segurança do Windows que tem as permissões de administrador global.

## <a name="modes-of-operation"></a>Modos de funcionamento
Pode executar a ferramenta nos seguintes dois modos. Recomendamos que execute a ferramenta *hipóteses* modo de modo a poder rever os resultados antes de executar a ferramenta no *eliminar modo*:
  1.    **Modo de hipóteses**:   
      Se não especificar o **/eliminar** comutador, a ferramenta é executada no modo de hipóteses e identifica o conteúdo que seria eliminado do ponto de distribuição.
   - Quando executar neste modo a ferramenta não elimina quaisquer dados.
   - As informações sobre o conteúdo que seria eliminado são escritas para o ficheiro de registo de ferramentas e não-á pedido para confirmar cada eliminação potencial.  
      </br>   

  2. **Eliminar modo**:   
    Quando executa a ferramenta com a **/eliminar** comutador, a ferramenta é executada no modo de eliminação.

     - Quando executar neste modo, conteúdo órfão que se encontra no ponto de distribuição especificado pode ser eliminado da biblioteca de conteúdos do ponto de distribuição.
     -     Antes de eliminar cada ficheiro, tem de confirmar que o ficheiro deve ser eliminado.  Pode selecionar, **Y** para Sim, **N** para não, ou **Sim a todos os** para ignorar avisos adicionais e eliminar conteúdo órfão tudo.  
     </br>

Quando a ferramenta é executada no modo de ambos, cria automaticamente um registo com um nome que inclua o modo da que ferramenta é executada no nome do ponto de distribuição e a data e hora da operação. O ficheiro de registo aberto automaticamente quando a ferramenta de conclusão.

Por predefinição, o ficheiro de registo é escrito para a pasta temporária da conta de utilizador que executa a ferramenta, no computador onde a ferramenta é executada. Pode utilizar o **/registo** comutador para redirecionar o ficheiro de registo para outra localização, incluindo uma partilha de rede.


## <a name="run-the-tool"></a>Execute a ferramenta
Para executar a ferramenta:
1. Abra uma linha de comandos administrativa para uma pasta que contém **ContentLibraryCleanup.exe**.  
2. Em seguida, introduza uma linha de comandos que inclui os parâmetros de linha de comandos necessário e parâmetros opcionais que pretende utilizar.

**Conhecido problema** quando a ferramenta é executada, poderá ser devolvido um erro semelhante ao seguinte quando qualquer pacote de implementação falhou ou está em curso:
-  *System.InvalidOperationException: Esta biblioteca de conteúdos não é possível limpar neste momento porque o pacote <packageID> não está completamente instalado.*

**Solução:** Nenhuma. A ferramenta não é possível fiável identificar ficheiros órfãos quando o conteúdo está em curso ou falhou implementar. Por conseguinte, a ferramenta não permitirá ao conteúdo de limpeza até que esse problema seja resolvido.

### <a name="command-line-switches"></a>Parâmetros de linha de comandos  
Os seguintes parâmetros de linha de comandos podem ser utilizados por qualquer ordem.   

|Parâmetro|Detalhes|
|---------|-------|
|**/DELETE**  |**Opcional** </br> Utilize este parâmetro quando pretender eliminar o conteúdo do ponto de distribuição. -Á antes do conteúdo é eliminado. </br></br> Quando este comutador não é utilizado, a ferramenta regista resultados sobre o conteúdo que seria eliminado, mas não eliminar o conteúdo do ponto de distribuição. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp Server1. contoso.com /delete*** |
| **/q**       |**Opcional** </br> Este parâmetro é executada a ferramenta num modo sossegado que suprime todos os avisos (como os pedidos para eliminar conteúdo) e não abre automaticamente o ficheiro de registo. </br></br> Exemplo: ***ContentLibraryCleanup.exe /q /dp Server1. contoso.com*** |
| **/dp &lt;FQDN do ponto de distribuição >**  | **Necessário** </br> Especifique o nome de domínio completamente qualificado (FQDN) do ponto de distribuição que pretende limpar. </br></br> Exemplo:  ***/Dp de ContentLibraryCleanup.exe Server1. contoso.com***|
| **/PS &lt;FQDN de site principal >**       | **Opcional** quando limpar conteúdo a partir de um ponto de distribuição num site primário.</br>**Obrigatório** quando limpar conteúdo a partir de um ponto de distribuição num site secundário. </br></br>A ferramenta de suporte de dados liga-se para o site primário principal para executar consultas no SMS_Provider. Estas permitem consultas a ferramenta de determinar que conteúdo deve ser no ponto de distribuição para que possa identificar o conteúdo que é órfã e pode ser removido. Esta ligação para o site primário principal têm de ser feita para pontos de distribuição num site secundário porque os detalhes necessários não estão disponíveis diretamente a partir do site secundário.</br></br> Especifique o FQDN do site primário que o ponto de distribuição pertence a ou do elemento principal primário principal quando o ponto de distribuição estiver num site secundário. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp Server1. contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;código do site principal >**  | **Opcional** quando limpar conteúdo a partir de um ponto de distribuição num site primário.</br>**Obrigatório** quando limpar conteúdo a partir de um ponto de distribuição num site secundário. </br></br> Especifique o código do site do site primário que o ponto de distribuição pertence a ou do site primário principal quando o ponto de distribuição estiver num site secundário.</br></br> Exemplo: ***ContentLibraryCleanup.exe /dp Server1. contoso.com /sc ABC*** |
| **/log<log file directory>**       |**Opcional** </br> Especifique a localização onde a ferramenta escreve o ficheiro de registo. Isto pode ser numa unidade local ou numa rede de partilhar.</br></br> Quando este comutador não é utilizado, o ficheiro de registo é colocado na pasta temp do utilizador, no computador onde a ferramenta é executada.</br></br> Exemplo de unidade local: ***ContentLibraryCleanup.exe /dp Server1. contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Exemplo de partilha de rede: ***ContentLibraryCleanup.exe /dp Server1. contoso.com /log \\ &lt;partilhar >\&lt; pasta >***|

