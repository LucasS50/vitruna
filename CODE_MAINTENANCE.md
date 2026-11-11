# Guia de manutenção do código — Vitruna

## Convenções de comentários

O código deve explicar **regras de negócio e decisões**, não repetir o que uma linha evidente já faz. Documentação de módulos usa comentários JSDoc, observações inline nos pontos sensíveis e testes que exemplificam os contratos. Alterações nas regras financeiras e tenant precisam atualizar integração e este mapa.

## Backend (NestJS)

| Caminho | Responsabilidade | Cuidado |
|---|---|---|
| `src/main.ts`, `src/http-security.ts` | inicialização e política HTTP | cookies, CORS, Origin e HTTPS |
| `src/modules/app.module.ts` | registro de dependências | incluir providers e controllers |
| `src/prisma/prisma.service.ts` | conexão com PostgreSQL | nunca confiar só no frontend |
| `src/auth/` | login, tokens, verificação, recuperação | rate-limit, token único e sessão segura |
| `src/admin/saas-management.controller.ts` | ADM Vitruna | SUPERADMIN da plataforma, não OWNER |
| `src/admin/saas.schemas.ts` | validação dos inputs do SaaS | entrada restrita, dinheiro em centavos |
| `src/billing/subscription-access.ts` | bloqueio por vencimento e carência | aplicar em todas as rotas privadas |
| `src/stores/store.controller.ts` | painel e marca do lojista | confirmar StoreMember/OWNER |
| `src/stores/public-store.controller.ts` | catálogo livre | retornar somente dados públicos |
| `src/catalog/` | categoria, produto, SKU, preço, estoque | filtro pelo storeId autenticado |
| `src/images/` | processamento e storage de fotos | 5 MiB, pixels, WebP e credenciais |
| `src/email/` | mensagens transacionais SMTP | não incluir tokens nos logs |
| `prisma/migrations/` | persistência versionada | sempre migration + teste |
| `scripts/bootstrap-saas-admin.mjs` | primeiro ADM | terminal confiável, nunca rota pública |

## Frontend (Next.js)

| Caminho | Responsabilidade | Cuidado |
|---|---|---|
| `src/app/page.tsx` | landing page comercial | não inventar preços/depoimentos |
| `src/app/[slug]/page.tsx` | catálogo aberto | jamais exigir login de visitante |
| `src/components/storefront-cart.tsx` | carrinho e WhatsApp | não afirmar venda/baixa de estoque |
| `src/lib/cart-utils.ts` | reconciliação de SKU/estoque | dados do localStorage não confiáveis |
| `src/components/product-gallery.tsx` | galeria | URLs remotas nunca como HTML |
| `src/app/painel/` | Superadmin da loja | acesso por membership validado no backend |
| `src/app/saas/admin/` | ADM Vitruna | exclusivo SUPERADMIN de plataforma |
| `src/components/dashboard-shell.tsx` | menus e layout por contexto | ocultar menu não é autorização |
| `src/lib/api.ts` | requisições HTTP | cookies HttpOnly e erros padronizados |

## Políticas de alteração

1. Alterar contrato da API e testar com PostgreSQL.
2. Atualizar consumidores do contrato no frontend.
3. Acrescentar comentários nos pontos de regra, não em cada instrução.
4. Executar CI em ambas as branches e validar visualmente no navegador.
5. Atualizar `ROADMAP.md` e só então considerar merge revisado.
