---
title: "A ferramenta de limpeza da biblioteca de conteúdos | Microsoft Docs"
description: "Utilize a ferramenta de limpeza da biblioteca de conteúdos para remover o conteúdo órfão já não está associado a uma implementação do System Center Configuration Manager."
ms.custom: na
ms.date: 4/7/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 76e6772bdd5cbd32d525e728f6ebc988b045da78
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="the-content-library-cleanup-tool-for-system-center-configuration-manager"></a>A ferramenta de limpeza da biblioteca de conteúdos para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 A partir da versão 1702, pode utilizar uma ferramenta de linha de comandos (**ContentLibraryCleanup.exe**) remover o conteúdo que é mais longo não associados a qualquer pacote ou aplicação a partir de um ponto de distribuição (órfão conteúdo). Esta ferramenta denomina-se a ferramenta de limpeza da biblioteca de conteúdos e substitui as versões anteriores das ferramentas semelhantes lançadas para produtos anteriores do Configuration Manager.  

A ferramenta afeta apenas o conteúdo no ponto de distribuição que especificou quando executa a ferramenta. A ferramenta não é possível remover o conteúdo da biblioteca de conteúdos no servidor do site.

Pode encontrar **ContentLibraryCleanup.exe** no *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* pasta no servidor do site num site de administração central ou site primário.

## <a name="requirements"></a>Requisitos  
 A ferramenta só pode executar em relação a um único ponto de distribuição de cada vez.  
 - Pode ser executado diretamente no computador que aloja o ponto de distribuição que pretende apagar ou remotamente a partir de outro servidor.
 - A conta de utilizador que executa a ferramenta tem de ter permissões de administração baseada em funções direta igual a um administrador total na hierarquia do Configuration Manager. A ferramenta não funciona quando a conta recebe estas permissões, como um membro de um grupo de segurança do Windows que tem as permissões de administrador global.

## <a name="modes-of-operation"></a>Modos de funcionamento
Pode executar a ferramenta no seguintes dois modos. Recomendamos que execute a ferramenta numa *investiguem* modo, pelo que pode rever os resultados antes de executar a ferramenta *eliminar modo*:
  1.    **Modo de investiguem**:   
      Se não especificar o **/eliminar** comutador, a ferramenta é executado no modo de investiguem e identifica os conteúdos que serão eliminados do ponto de distribuição.
   - Quando executado no modo a ferramenta não elimina quaisquer dados.
   - Informações sobre o conteúdo que será eliminado são escritas no ficheiro de registo de ferramentas e não lhe para confirmar eliminação cada potencial.  
      </br>   

  2. **Eliminar modo**:   
    Quando executa a ferramenta com o **/eliminar** comutador, a ferramenta é executada no modo de eliminação.

     - Quando são executados neste modo, o conteúdo órfão que se encontra no ponto de distribuição especificado pode ser eliminado da biblioteca de conteúdos do ponto de distribuição.
     -  Antes de eliminar cada ficheiro, tem de confirmar que o ficheiro deve ser eliminado.  Pode selecionar, **Y** para Sim, **N** para não, ou **Sim para todas as** para ignorar avisos adicionais e eliminar todos os órfão conteúdo.  
     </br>

Quando a ferramenta é executada em qualquer modo, cria automaticamente um registo com um nome que inclui o modo da que ferramenta é executada, o nome do ponto de distribuição e a data e hora da operação. O ficheiro de registo abre automaticamente quando a ferramenta estiver concluída.

Por predefinição, o ficheiro de registo é escrito na pasta temporária da conta de utilizador que executa a ferramenta, no computador onde a ferramenta é executada. Pode utilizar o **/iniciar sessão** comutador para redirecionar o ficheiro de registo para outra localização, incluindo uma partilha de rede.


## <a name="run-the-tool"></a>Execute a ferramenta
Para executar a ferramenta:
1. Abra uma linha de comandos administrativa para uma pasta que contém **ContentLibraryCleanup.exe**.  
2. Em seguida, introduza uma linha de comandos que inclui os comutadores de linha de comandos necessário e comutadores opcionais que pretende utilizar.

**Problema de conhecido** quando a ferramenta é executada, poderá ser devolvido um erro semelhante ao seguinte, quando qualquer pacote de implementação falhou ou está em curso:
-  *System.InvalidOperationException: Nesta biblioteca de conteúdos não é possível limpar neste momento porque o pacote <packageID> não é completamente instalado.*

**Solução:** Nenhuma. A ferramenta não é possível fiável identificar ficheiros órfãos quando o conteúdo está em curso ou falhou a implementação. Por conseguinte, a ferramenta não permitirá a limpar conteúdo até que este problema seja resolvido.

### <a name="command-line-switches"></a>Parâmetros da linha de comandos  
Os seguintes parâmetros de linha de comandos podem ser utilizados por qualquer ordem.   

|Parâmetro|Detalhes|
|---------|-------|
|**/DELETE**  |**Opcional** </br> Utilize este parâmetro se pretender eliminar o conteúdo do ponto de distribuição. Lhe for pedido antes do conteúdo é eliminado. </br></br> Quando este parâmetro não for utilizado, a ferramenta regista resultados sobre o conteúdo que será eliminado, mas não eliminar o conteúdo do ponto de distribuição. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Opcional** </br> Este comutador este último executa a ferramenta de um modo silencioso que suprime todos os avisos (como os pedidos para eliminar conteúdo) e não automaticamente a abrir o ficheiro de registo. </br></br> Exemplo: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;FQDN do ponto de distribuição >**  | **Necessário** </br> Especifique o nome de domínio completamente qualificado (FQDN) do ponto de distribuição que pretende apagar. </br></br> Exemplo:  ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/PS &lt;site primário FQDN >**       | **Opcional** quando o conteúdo a partir de um ponto de distribuição num site primário de limpeza.</br>**Necessário** quando o conteúdo a partir de um ponto de distribuição num site secundário de limpeza. </br></br>A ferramenta estabelece ligação ao site primário principal para executar consultas no SMS_Provider. Estas permitem consultas a ferramenta de determinar o conteúdo que deve estar no ponto de distribuição, para que possa identificar o conteúdo que é órfã e pode ser removido. Esta ligação para o site primário principal tem de ser feita para pontos de distribuição num site secundário porque os detalhes necessários não estão disponíveis diretamente a partir do site secundário.</br></br> Especifique o FQDN do site primário que pertence o ponto de distribuição ou de principal primário principal quando o ponto de distribuição num site secundário. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;código do site principal >**  | **Opcional** quando o conteúdo a partir de um ponto de distribuição num site primário de limpeza.</br>**Necessário** quando o conteúdo a partir de um ponto de distribuição num site secundário de limpeza. </br></br> Especifique o código do site do site primário que pertence o ponto de distribuição ou do site primário principal quando o ponto de distribuição num site secundário.</br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log<log file directory>**       |**Opcional** </br> Especifique a localização onde a ferramenta escreve o ficheiro de registo. Isto pode ser uma unidade local ou numa rede de partilha.</br></br> Quando este parâmetro não for utilizado, o ficheiro de registo é colocado na pasta temporária do utilizador, no computador onde a ferramenta é executada.</br></br> Exemplo de unidade local: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Exemplo de partilha de rede: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\ &lt;partilhar >\&lt; pasta >***|
