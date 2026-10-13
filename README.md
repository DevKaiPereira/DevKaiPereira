<!-- TEMPLATE: copie para o README.md de cada projeto e troque o que estiver em MAIÚSCULAS -->

<div align="center">

# NOME DO PROJETO

**Uma frase que explica o que o projeto resolve.**

<img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" />
<img src="https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white" />
<img src="https://img.shields.io/badge/licen%C3%A7a-MIT-blue?style=flat-square" />
<img src="https://img.shields.io/github/last-commit/DevKaiPereira/NOME-DO-REPO?style=flat-square" />

[🌐 Demo ao vivo](https://LINK-DO-DEPLOY) · [🐞 Reportar bug](https://github.com/DevKaiPereira/NOME-DO-REPO/issues) · [💡 Sugerir melhoria](https://github.com/DevKaiPereira/NOME-DO-REPO/issues)

<!-- Coloque aqui um print ou GIF do projeto funcionando. É o que mais chama atenção. -->
<img src="./docs/preview.gif" alt="Demonstração do projeto" width="85%" />

</div>

---

## 📖 Sobre

Explique em 3 ou 4 linhas:
- **Qual problema** o projeto resolve
- **Para quem** ele serve
- **Por que** você decidiu construí-lo

## ✨ Funcionalidades

- [x] Funcionalidade 1
- [x] Funcionalidade 2
- [x] Funcionalidade 3
- [ ] Próxima funcionalidade planejada

## 🛠️ Tecnologias

| Camada | Tecnologia |
|---|---|
| Linguagem | TypeScript |
| Back-end | Node.js, Express |
| Banco de dados | PostgreSQL, Prisma |
| Validação | Zod |
| Testes | Vitest / Jest |

## 🧱 Arquitetura

```
src/
├── controllers/   # recebem a requisição e devolvem a resposta
├── services/      # regras de negócio
├── repositories/  # acesso ao banco de dados
├── middlewares/   # autenticação, tratamento de erros
├── routes/        # definição das rotas
└── tests/         # testes automatizados
```

## 🚀 Como rodar

**Pré-requisitos:** Node.js 20+ e npm.

```bash
# 1. Clone o repositório
git clone https://github.com/DevKaiPereira/NOME-DO-REPO.git
cd NOME-DO-REPO

# 2. Instale as dependências
npm install

# 3. Configure as variáveis de ambiente
cp .env.example .env

# 4. Rode em desenvolvimento
npm run dev
```

### Variáveis de ambiente

| Variável | Descrição | Exemplo |
|---|---|---|
| `PORT` | Porta do servidor | `3333` |
| `DATABASE_URL` | URL do banco de dados | `postgresql://...` |
| `JWT_SECRET` | Chave de autenticação | `sua-chave-secreta` |

## 🔌 Endpoints (se for uma API)

| Método | Rota | Descrição |
|---|---|---|
| `POST` | `/users` | Cria um usuário |
| `POST` | `/sessions` | Autentica o usuário |
| `GET` | `/refunds` | Lista solicitações |
| `POST` | `/refunds` | Cria uma solicitação |

## 🧪 Testes

```bash
npm run test
```

## 📚 O que aprendi

- Aprendizado técnico 1 (ex.: organizar o projeto em camadas)
- Aprendizado técnico 2 (ex.: validar dados com Zod)
- Desafio que enfrentei e como resolvi

## 🗺️ Próximos passos

- [ ] Adicionar testes automatizados
- [ ] Configurar CI com GitHub Actions
- [ ] Fazer deploy

## 👤 Autor

**Kaique Pereira**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/dev-kaique)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/DevKaiPereira)

## 📄 Licença

Distribuído sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.
