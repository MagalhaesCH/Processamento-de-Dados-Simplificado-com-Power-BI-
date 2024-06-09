### Desafio Módulo 3 – Processamento de Dados Simplificado com Power BI

Neste desafio, você aprenderá a configurar uma instância de MySQL na Azure, integrar com o Power BI e realizar a transformação dos dados para preparar um relatório analítico. Seguindo as diretrizes abaixo, você conseguirá concluir cada etapa do desafio com sucesso.

### Etapas do Desafio

#### 1. Criação de uma Instância na Azure para MySQL
1. **Acessar o Portal Azure**: Entre no portal Azure utilizando suas credenciais.
2. **Criar um Banco de Dados MySQL**:
    - Navegue até "Criar um recurso" > "Bancos de Dados" > "Banco de Dados MySQL".
    - Configure o nome do servidor, grupo de recursos, região e credenciais de administrador.
    - Selecione o nível de desempenho adequado (Basic, General Purpose, ou Memory Optimized).
    - Conclua a criação e espere até que o servidor esteja pronto.

#### 2. Criar o Banco de Dados com Base Disponível no GitHub
1. **Clonar o Repositório do GitHub**: Clone ou baixe os arquivos do repositório que contém o script SQL para a criação do banco de dados.
2. **Acessar o Servidor MySQL**:
    - Utilize um cliente MySQL (como MySQL Workbench) para conectar-se ao servidor MySQL na Azure.
    - Conecte-se usando o endereço do servidor, nome de usuário e senha criados anteriormente.
3. **Executar o Script SQL**:
    - Carregue o script SQL no cliente MySQL.
    - Execute o script para criar e popular o banco de dados com os dados fornecidos.

#### 3. Integração do Power BI com MySQL no Azure
1. **Abrir o Power BI Desktop**: Inicie o Power BI Desktop em seu computador.
2. **Conectar ao MySQL na Azure**:
    - Selecione "Obter Dados" > "Banco de Dados MySQL".
    - Insira o nome do servidor, nome do banco de dados, nome de usuário e senha.
    - Clique em "OK" para conectar.
3. **Importar Dados**:
    - Selecione as tabelas que deseja importar.
    - Carregue os dados para o Power BI.

#### 4. Verificar Problemas na Base para Realizar a Transformação dos Dados
### Diretrizes para Transformação dos Dados

#### 1. Verifique os Cabeçalhos e Tipos de Dados
1. **Revisar os Nomes das Colunas**: Certifique-se de que os cabeçalhos das colunas estejam corretos e autoexplicativos.
2. **Verificar os Tipos de Dados**:
    - Abra o Editor de Consultas no Power BI.
    - Revise e ajuste os tipos de dados conforme necessário (por exemplo, datas, números inteiros, texto).

#### 2. Modifique os Valores Monetários para o Tipo Double Preciso
1. **Localizar Colunas Monetárias**: Identifique as colunas que contêm valores monetários.
2. **Alterar o Tipo de Dados**:
    - No Editor de Consultas, selecione a coluna.
    - Alterar o tipo de dados para "Decimal Number" (ou Double).

#### 3. Verifique a Existência de Valores Nulos e Analise a Remoção
1. **Identificação de Valores Nulos**:
    - Use a funcionalidade de filtro no Editor de Consultas para identificar valores nulos.
2. **Decisão sobre Remoção ou Substituição**:
    - Avalie se os dados nulos podem ser removidos sem perder informações críticas.
    - Caso contrário, considere substituí-los por valores padrão (por exemplo, 0 para números, "Desconhecido" para texto).

#### 4. Employees com Nulos em Super_ssn Podem Ser Gerentes
1. **Identificação de Gerentes**:
    - Filtre a tabela de funcionários (employees) para identificar registros com valores nulos em `Super_ssn`.
    - Confirme se esses registros representam gerentes.
2. **Verificação de Colaboradores Sem Gerente**:
    - Garanta que todos os colaboradores tenham um gerente associado. Corrija registros onde necessário.

#### 5. Verifique se Há Algum Departamento Sem Gerente
1. **Identificação de Departamentos Sem Gerente**:
    - Revise a tabela de departamentos para identificar qualquer departamento sem um gerente associado.

#### 6. Se Houver Departamento sem Gerente, Preencha as Lacunas
1. **Atribuição de Gerentes**:
    - Se algum departamento estiver sem gerente, assuma que você tem os dados e preencha esses registros.

#### 7. Verifique o Número de Horas dos Projetos
1. **Validação dos Dados de Horas**:
    - Verifique a consistência e plausibilidade dos dados de horas trabalhadas nos projetos.

#### 8. Separar Colunas Complexas
1. **Divisão de Colunas**:
    - Identifique colunas que contêm múltiplos valores ou informações concatenadas.
    - Use a funcionalidade de dividir colunas no Editor de Consultas para separar essas informações.

#### 9. Mesclar Consultas Employee e Department para Criar uma Tabela Employee com Nome dos Departamentos
1. **Mesclagem de Tabelas**:
    - No Editor de Consultas, mescle a tabela de funcionários com a tabela de departamentos.
    - Utilize uma junção esquerda (Left Join) para garantir que todos os funcionários estejam incluídos.
2. **Eliminação de Colunas Desnecessárias**:
    - Após a mesclagem, remova colunas redundantes ou desnecessárias.

#### 10. Realize a Junção dos Colaboradores e Respectivos Nomes dos Gerentes
1. **Junção de Dados**:
    - Use uma consulta SQL ou a funcionalidade de mesclagem do Power BI para associar cada colaborador com o nome de seu gerente.
    - Se usar SQL, documente a query utilizada no README.
2. **Exemplo de Query SQL**:
    ```sql
    SELECT e.emp_no, e.first_name, e.last_name, d.dept_name, m.first_name AS manager_first_name, m.last_name AS manager_last_name
    FROM employees e
    LEFT JOIN departments d ON e.dept_no = d.dept_no
    LEFT JOIN employees m ON e.manager_no = m.emp_no;
    ```

#### 11. Mescle Colunas de Nome e Sobrenome
1. **Combinação de Nomes**:
    - No Editor de Consultas, crie uma nova coluna concatenando as colunas de nome e sobrenome.

#### 12. Mescle Nomes de Departamentos e Localização
1. **Criação de Combinações Únicas**:
    - Combine os nomes dos departamentos com suas localizações para criar uma nova coluna única.

#### 13. Explique por que Utilizar Mesclar e Não Atribuir
1. **Preservação de Dados**:
    - A mesclagem cria novas colunas sem alterar os dados existentes, enquanto atribuir pode sobrescrever informações. Mesclar é preferível para garantir a integridade dos dados.

#### 14. Agrupe os Dados para Saber Quantos Colaboradores Existem por Gerente
1. **Agrupamento de Dados**:
    - No Editor de Consultas, agrupe os dados pela coluna de gerentes e conte o número de colaboradores em cada grupo.

#### 15. Elimine Colunas Desnecessárias
1. **Revisão Final**:
    - Revise todas as tabelas e remova colunas que não serão utilizadas no relatório final para manter os dados limpos e organizados.

### Conclusão
Seguindo essas diretrizes, você conseguirá criar um portfólio de dados limpo e bem estruturado, pronto para análise no Power BI. Certifique-se de documentar cada passo do processo e de verificar a consistência e precisão dos dados transformados.

---

### Ferramentas e Recursos
- **Azure Portal**: Para a criação da instância MySQL.
- **GitHub**: Para o script de criação do banco de dados.
- **MySQL Workbench**: Para gerenciar o banco de dados MySQL.
- **Power BI Desktop**: Para a integração e transformação dos dados.

