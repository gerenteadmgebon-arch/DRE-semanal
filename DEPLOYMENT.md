# DRE compartilhado — ativação pendente

O modelo compartilhado de Editor/Leitor foi preparado e testado; sua ativação no Firebase permanece pendente de confirmação. Os ajustes de interface já foram publicados separadamente em produção, mantendo a autenticação e o acesso ao banco existentes.

## Comportamento

- Editor tem as mesmas permissões funcionais do administrador, inclusive gestão de usuários. Leitor somente consulta. O proprietário fixo não pode ser bloqueado.
- E-mails existentes sem perfil explícito passam a ser leitores. A promoção para Editor deve ser feita no cadastro de usuários.
- Um rascunho compartilhado em `gebonDreDrafts/shared_completo`, diários compartilhados por empresa e competência, e histórico comum. UID/e-mail são autoria, não separação dos dados.
- O último rascunho legado é carregado quando ainda não existe rascunho compartilhado. Diários legados são aproveitados na primeira gravação compartilhada; arquivos antigos ficam preservados e sem novas gravações.
- Transações com revisão bloqueiam sobrescrita concorrente. Alterações externas chegam em tempo real; se há edição local pendente, a interface pede recarregamento.
- Visão geral usa data inicial/final. Meses inteiros usam o fechamento; partes do mês usam lançamentos diários. Ajustes mensais sem data não são distribuídos artificialmente. Taxa manual mensal não é aplicada automaticamente a um recorte diário com base financeira não nula; nesse caso o sistema orienta usar CDI automático.
- Excel: duas casas em valores, zeros e percentuais, inclusive Dias salvos; taxas são exportadas como porcentagens numéricas.
- Formulário rápido com largura de 470 px, campos em uma coluna e somente as datas lado a lado; menus Importar planilha, Baixar modelo Excel e Relatórios e exportação removidos.
- Estrutura: competência, Excel e Resumo do dia juntos; um único Salvar concilia os lançamentos diários e o Realizado. Empresa e o quadro separado de datas/dias salvos foram removidos. A data continua no cabeçalho da coluna DIA.
- Resumo do dia usa o renderizador SVG/PNG do DRE simplificado, movimentos apenas da data, saldos cronológicos e CDI apurado para um único dia. Valores e ajustes mensais sem data não entram na movimentação diária.

## Validação

21 verificações no emulador Firestore, incluindo gravação bruta recusada para leitor, edição comum, atualização em tempo real, conflito, migração legada, autorização do Editor e rebaixamento de perfil. Testes de intervalo, saldos, comparativos, Excel e 348 valores do modelo original passaram. Interface de Editor e Leitor foi conferida com dados fictícios.

## Ordem de ativação

1. Obter confirmação final para ampliar o acesso aos dados financeiros compartilhados, exigida pelo controle do navegador.
2. Conferir e publicar o arquivo firestore.rules no projeto Firebase gebon-portal-financeiro. Não publicar regras de outros projetos.
3. Publicar index.html desta branch em main de DRE-semanal e a branch de mesmo nome em main de financeiro.
4. Conferir os dois deploys do GitHub Pages. Recarregar abas antigas, que não podem continuar gravando no modelo separado.

A publicação intermediária anterior foi rejeitada. Depois foram publicados dois ajustes autorizados e compatíveis com as permissões atuais: remoção de menus (459cef719b1210e065c5df32380b222a8dd48367) e controles/resumo diário/formulário/data inicial-final/Excel (77cb0b064d3228aeb07ced2b10ccd4dd16a7e625). Esta branch já incorpora todos esses ajustes. Consulte o SHA atual de main antes da ativação e preserve as alterações posteriores.
