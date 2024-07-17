# Canvas de Mapeamento de Fontes de Dados

## Instruções de Preenchimento

Preencha cada seção deste canvas para mapear as fontes de dados relevantes para a solução de IA. Este documento ajudará a identificar e organizar as fontes de dados necessárias para a construção e treinamento do modelo de IA.

### 1. Nome da Fonte de Dados

- **Instruções:** Identifique e nomeie cada fonte de dados relevante. Este nome deve ser claro e descritivo para facilitar a referência.
- **Exemplo:** Base de Dados de Agendamentos de Consultas

### 2. Descrição da Fonte de Dados

- **Instruções:** Descreva brevemente a fonte de dados, incluindo o tipo de dados que ela contém e o seu propósito no contexto da solução de IA.
- **Exemplo:** Base de dados contendo informações sobre agendamentos de consultas médicas, incluindo detalhes como data, hora, médico, paciente e status da consulta.

### 3. Origem dos Dados

- **Instruções:** Indique de onde os dados são originados. Pode incluir sistemas internos, fontes externas, dispositivos IoT, etc.
- **Exemplo:** Sistema de gestão de clínicas, registros de chamadas telefônicas de agendamento.

### 4. Tipo de Dados

- **Instruções:** Classifique o tipo de dados contidos na fonte. Pode ser texto, numérico, temporal, categórico, etc.
- **Exemplo:** Dados numéricos (número de consultas), dados textuais (nomes de pacientes e médicos), dados temporais (datas e horários).

### 5. Formato dos Dados

- **Instruções:** Descreva o formato dos dados na fonte. Isso pode incluir formatos de arquivos (CSV, JSON, SQL), esquemas de banco de dados, etc.
- **Exemplo:** Arquivo CSV com colunas para data, hora, médico, paciente e status; banco de dados SQL com tabelas correspondentes.

### 6. Frequência de Atualização

- **Instruções:** Especifique a frequência com que os dados são atualizados. Pode ser em tempo real, diária, semanal, mensal, etc.
- **Exemplo:** Atualização em tempo real com cada novo agendamento inserido no sistema.

### 7. Qualidade dos Dados

- **Instruções:** Avalie a qualidade dos dados na fonte. Considere a completude, precisão, e a presença de dados faltantes ou errôneos.
- **Exemplo:** Dados geralmente completos, com algumas entradas com informações faltantes que precisam ser limpas.

### 8. Métodos de Coleta

- **Instruções:** Descreva como os dados são coletados. Importação de arquivos, chamadas de API, inserção manual, etc.
- **Exemplo:** Importação automática via API

### 9. Acesso aos Dados

- **Instruções:** Descreva como os dados podem ser acessados. Isso inclui APIs, interfaces de usuário, conexões de banco de dados, etc.
- **Exemplo:** Acesso via API REST fornecida pelo sistema de gestão de clínicas; exportação manual de arquivos CSV.

### 10. Proprietário dos Dados

- **Instruções:** Identifique o proprietário ou responsável pela fonte de dados. Pode ser uma pessoa, um departamento, ou uma organização.
- **Exemplo:** Departamento de TI da Clínica

### 11. Restrições de Privacidade e Segurança

- **Instruções:** Identifique quaisquer restrições relacionadas à privacidade e segurança dos dados. Considere regulamentações e políticas internas.
- **Exemplo:** Dados sensíveis de pacientes precisam de criptografia durante a transmissão e armazenamento, conforme regulamentações de proteção de dados pessoais.

### 12. Requisitos de Integração

- **Instruções:** Liste os requisitos técnicos para integrar os dados da fonte com a solução de IA. Inclua considerações sobre transformação de dados, compatibilidade e sincronização.
- **Exemplo:** Necessidade de transformação de dados de CSV para JSON para integração com o modelo de IA; sincronização diária com a base de dados de agendamentos.
