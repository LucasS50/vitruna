# Arquitetura Vitruna — ADR-001

## Decisão

Manter frontend e backend em repositórios e deploys independentes. A documentação do produto fica em `vitruna-docs`. A identidade visual base usa off-white, rosé discreto, grafite, tipografia editorial e componentes acessíveis.

## Frontend

- Next.js App Router, React e TypeScript.
- Deploy independente; porta 3000 em desenvolvimento.
- Acesso à API por HTTPS com credenciais de sessão HttpOnly. Nunca acessar banco diretamente.
- Rotas iniciais: `/`, `/cadastro`, `/entrar`, `/verificar-email`, `/painel`, `/saas/admin`, `/saas/admin/dashboard`.
- A UI nunca substitui autorização do servidor.

## Backend

- NestJS, Prisma 6 e PostgreSQL 16.
- Porta 4000 em desenvolvimento, prefixo `/api/v1`.
- Sessões opacas com token aleatório e SHA-256 no banco; senhas Argon2id.
- Contas, lojas e membros com funções OWNER, MANAGER, ATTENDANT. Role de plataforma SUPERADMIN separado.
- Endpoints iniciais:
  - GET `/health/live`
  - GET `/health/ready`
  - POST `/auth/register`
  - POST `/auth/verify-email`
  - POST `/auth/login`
  - POST `/auth/logout`
  - GET `/auth/me`
  - GET `/stores/me`
  - GET `/admin/summary`

## Multi-tenancy

Cada loja tem UUID e slug único. Relações de usuários via StoreMember. As APIs privadas nunca devem confiar em `storeId` ou `x-tenant` fornecidos sem validação de associação. Produtos, estoque, pedidos e cobrança terão FK de `storeId` e RLS no PostgreSQL em migrações futuras, com acesso utilizando role de execução sem BYPASSRLS.

## Catálogo e WhatsApp

Carrinho não reserva estoque; abertura do WhatsApp não comprova mensagem enviada ou compra concluída. Pedido só deve ser baixado do estoque após confirmação registrada, com idempotência e concorrência controlada.

## Contratos

Frontend comunica-se apenas com a API versionada. Mudanças de contratos devem incluir documentação e testes, e sua compatibilidade deve ser conferida antes da publicação de ambos os serviços.

## Status

A Fase 1 é uma **fundação parcial executável**, sujeita à instalação, migrações, integração e testes. Não declarar as 63 telas como prontas.
