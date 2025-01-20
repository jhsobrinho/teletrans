# Transcribe - Sistema de Transcrição Médica

## Visão Geral
Sistema de transcrição médica que permite aos médicos gravar ou digitar textos e formatá-los de acordo com diferentes tipos de documentos médicos (consultas, retornos, exames, laudos, atestados e receitas).

## Estrutura do Projeto

### Frontend (React + TypeScript)
```
frontend/
├── src/
│   ├── components/
│   │   ├── transcription/
│   │   │   ├── NewTranscription.tsx    # Componente principal de transcrição
│   │   │   └── TranscriptionList.tsx   # Lista de transcrições
│   │   ├── auth/                       # Componentes de autenticação
│   │   └── common/                     # Componentes compartilhados
│   ├── services/                       # Serviços de API
│   └── contexts/                       # Contextos React
```

### Backend (Node.js + TypeScript)
```
backend/
├── src/
│   ├── controllers/                    # Controladores da API
│   ├── middlewares/                    # Middlewares (auth, logs)
│   ├── migrations/                     # Migrações do banco de dados
│   └── services/                       # Lógica de negócio
```

## Estrutura do Banco de Dados

### Tabela: users
- id (UUID): Identificador único
- name (VARCHAR): Nome do usuário
- email (VARCHAR): Email único
- password (VARCHAR): Senha criptografada
- role (VARCHAR): Papel do usuário (admin/doctor/owner)
- plan_id (UUID): Referência ao plano
- created_at (TIMESTAMP)
- updated_at (TIMESTAMP)

### Tabela: plans
- id (UUID): Identificador único
- name (VARCHAR): Nome do plano
- description (TEXT): Descrição do plano
- price (DECIMAL): Preço do plano
- max_transcriptions (INTEGER): Limite de transcrições
- active (BOOLEAN): Status do plano
- created_at (TIMESTAMP)
- updated_at (TIMESTAMP)

### Tabela: transcriptions
- id (UUID): Identificador único
- user_id (UUID): Referência ao usuário
- patient_name (VARCHAR): Nome do paciente
- transcription_text (TEXT): Texto original
- transcricao_ia (TEXT): Texto formatado pela IA
- document_type (VARCHAR): Tipo do documento
- created_at (TIMESTAMP)
- updated_at (TIMESTAMP)

### Tabela: transcription_settings
- id (UUID): Identificador único
- user_id (UUID): Referência ao usuário
- prompt_template (TEXT): Template do prompt
- document_type (VARCHAR): Tipo do documento
- created_at (TIMESTAMP)
- updated_at (TIMESTAMP)

## Funcionalidades Principais

### 1. Transcrição de Áudio
- Gravação de áudio em tempo real
- Conversão de fala para texto usando Web Speech API
- Suporte a diferentes navegadores

### 2. Formatação de Texto
- Formatação automática usando OpenAI
- Templates específicos por tipo de documento:
  - Consulta: Queixa Principal, História, Exame Físico, etc.
  - Retorno: Evolução, Resposta ao tratamento, etc.
  - Exame: Tipo, Achados, Conclusão
  - Laudo: Identificação, História, Conclusão
  - Atestado: Identificação, CID, etc.
  - Receita: Medicamentos, Posologia, etc.

### 3. Gerenciamento de Usuários
- Cadastro e autenticação
- Níveis de acesso (admin/doctor/owner)
- Gerenciamento de planos e limites

### 4. Configurações Personalizadas
- Templates de prompt por tipo de documento
- Configurações de formatação
- Preferências de usuário

## APIs e Endpoints

### Autenticação
- POST /auth/login
- POST /auth/register
- GET /auth/verify

### Transcrições
- POST /transcriptions
- GET /transcriptions
- PUT /transcriptions/:id
- DELETE /transcriptions/:id

### Usuários
- GET /users
- PUT /users/:id
- DELETE /users/:id

### Planos
- GET /plans
- POST /plans
- PUT /plans/:id
- DELETE /plans/:id

## Tecnologias Utilizadas

### Frontend
- React
- TypeScript
- Material-UI
- Axios
- Web Speech API

### Backend
- Node.js
- TypeScript
- Express
- TypeORM
- PostgreSQL
- OpenAI API

## Segurança
- JWT para autenticação
- Bcrypt para criptografia de senhas
- Middleware de autenticação
- Validação de entrada
- Rate limiting

## Monitoramento
- Logs de sistema
- Logs de transcrição
- Monitoramento de uso
- Alertas de erro

## Implantação
- Docker para containerização
- Scripts de migração
- Backup automático
- Configurações de ambiente

## Requisitos do Sistema
- Node.js 18+
- PostgreSQL 14+
- NPM ou Yarn
- Conexão com internet

## Configuração do Ambiente
1. Clone o repositório
2. Configure as variáveis de ambiente
3. Instale as dependências
4. Execute as migrações
5. Inicie o servidor

## Variáveis de Ambiente
```env
# Banco de Dados
DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASS=******
DB_NAME=transcribe

# OpenAI
OPENAI_API_KEY=sk-*****

# JWT
JWT_SECRET=******

# Servidor
PORT=3000
NODE_ENV=development
```

## Manutenção
- Backup diário do banco
- Monitoramento de recursos
- Atualização de dependências
- Rotação de logs
"# teletrans" 
