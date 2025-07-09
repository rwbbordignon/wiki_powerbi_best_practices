# Boas Práticas para Usuários de Power BI

---

### 1. Entenda o Propósito do Relatório
- **Por que o relatório existe?** Antes de mergulhar nos números, entenda quais perguntas o relatório responde e quais decisões ele deve apoiar.
- **Conheça os KPIs:** Familiarize-se com os principais indicadores (KPIs) e métricas apresentados. Se tiver dúvidas sobre o que algo significa, pergunte!

### 2. Aprenda os Conceitos Básicos
- **Termos essenciais:** Entenda o que são **medidas**, **dimensões**, **filtros** e **agregações**. Esse conhecimento básico ajuda a interpretar os dados corretamente e a fazer análises mais profundas.
- **Interatividade:** Explore os filtros e os elementos visuais clicáveis. Um bom relatório é desenhado para ser interativo.

### 3. Evite o "Ctrl+C, Ctrl+V" do Excel
- **Use o Power BI:** O Power BI foi criado para responder perguntas de negócio diretamente na ferramenta. Evite a tentação de exportar tabelas para o Excel para então começar sua análise.
- **Faça perguntas aos dados:** Use os filtros, explore os gráficos e, se precisar de um novo ângulo, solicite uma melhoria no relatório.

# Boas Práticas para Desenvolvedores de Power BI

Principais práticas para otimizar seus relatórios, garantindo performance, manutenibilidade e uma excelente experiência para o usuário final.

---

### 1. Otimize o Modelo de Dados
- **Mantenha o essencial:** Remova colunas e tabelas que não são utilizadas em visuais ou cálculos. Um modelo limpo é um modelo rápido.
- **Prefira Medidas DAX:** Evite colunas calculadas sempre que possível. Elas consomem memória e podem degradar a performance. Use medidas, que são calculadas em tempo de execução.
- **Tipos de dados corretos:** Ajuste os tipos de dados para economizar espaço. Evite texto de alta cardinalidade ou datas com hora se apenas a data for necessária.

### 2. Escreva DAX Eficiente
- **Medidas em vez de colunas:** Reforçando: use medidas para cálculos dinâmicos.
- **Cuidado com iteradores:** Funções como `SUMX` e `AVERAGEX` são poderosas, mas percorrem tabelas linha a linha. Use-as com critério, especialmente em tabelas grandes.
- **Evite `FILTER` desnecessário:** Muitas vezes, um `CALCULATE` com um filtro booleano simples (`KEEPFILTERS`) é mais performático do que usar a função `FILTER`.

### 3. Gerencie as Atualizações de Dados
- **Frequência ideal:** Nem todo relatório precisa ser atualizado a cada hora. Agende as atualizações de acordo com a necessidade do negócio e a frequência com que os dados de origem mudam.
- **Atualização incremental:** Para grandes volumes de dados históricos, configure a atualização incremental. Isso atualiza apenas os dados novos, reduzindo drasticamente o tempo de atualização.
- **Filtre na origem:** Use o Power Query para filtrar os dados o mais cedo possível, idealmente na própria fonte (ex: usando uma cláusula `WHERE` em SQL). Carregue apenas o que for necessário.

### 4. Use o Power Query com Eficiência
- **Remova etapas desnecessárias:** Revise o painel "Etapas Aplicadas" e remova ou combine passos que não agregam valor.
- **Filtre e ordene cedo:** Realize operações de filtragem e ordenação no início do processo de transformação para otimizar os passos subsequentes.
- **"Query Folding":** Sempre que possível, garanta que suas transformações no Power Query sejam convertidas em uma única consulta na fonte de dados (ex: uma única instrução SQL). Isso é muito mais performático.

### 5. Evite Visualizações Pesadas
- **Menos é mais:** Limite o número de visuais em uma única página (recomenda-se até 8). Muitas visualizações sobrecarregam o relatório.
- **Cuidado com a cardinalidade:** Evite gráficos ou tabelas com milhares de pontos de dados (ex: uma tabela com todas as vendas individuais). Agregue os dados ou forneça opções de drill-down.
- **Visuais otimizados:** Dê preferência aos visuais nativos. Se usar visuais personalizados da loja, verifique se são certificados e otimizados para performance.
- **Aplica conceitos de análise de dados e storytelling:** Como, por exemplo, 3,30,300 sendo a visualização que demora até 3 segundos para entender, 30 segundos para uma informação mais elaborada e justificada, e 300  segundos para algum analytics no detalhe. Outro conceito é construção em formato de Z, da informação mais relevante para a menos relevante, contando uma história conforme flui o BI.

### 6. Teste e Monitore a Performance
- **Use o Analisador de Desempenho:** No Power BI Desktop, em **Exibição > Analisador de Desempenho** para identificar quais visuais e medidas estão demorando mais para carregar.
- **Meça os tempos:** Avalie o tempo de carregamento de cada elemento e o tempo de resposta das interações (filtros, cliques).
- **Valide com os usuários:** A melhor forma de testar a experiência é com usuários reais. Observe como eles interagem e peça feedback sobre a velocidade e a usabilidade.

### 7. Respeite a Sensibilidade dos Dados
- **Privacidade em primeiro lugar:** Esteja ciente de que muitos relatórios contêm informações sensíveis e confidenciais.
- **Acesso não é sinônimo de compartilhamento:** O fato de você ter acesso a um relatório não significa que pode compartilhá-lo ou exportar seus dados para qualquer pessoa. Siga sempre as políticas de segurança da informação da sua empresa.

___

## Considerações Finais


*   **Power BI é a ferramenta de ponta, não a fábrica de dados:** Sua principal função é a visualização e exploração de dados já preparados. Ele não deve ser a principal ferramenta para transformações complexas (ETL) ou armazenamento de dados em larga escala.
    
*   **A base é o ETL e o Data Warehouse:** As boas práticas de governança de dados exigem que as transformações pesadas, a limpeza e a estruturação das informações ocorram em um ambiente dedicado (como um Data Warehouse). Isso garante que os dados sejam consistentes, rastreáveis e confiáveis antes de chegarem ao usuário final.
    
*   **Governança garante a integridade:** Utilizar um ambiente analítico apropriado para o ETL assegura que os processos sejam monitorados e auditáveis, um pilar essencial para a segurança e a conformidade dos dados."

_Diagrama ICEBERG apenas do Power BI_

![image](https://github.com/user-attachments/assets/e4db8d3e-76ee-45fb-8f08-fb68f80977ca)
