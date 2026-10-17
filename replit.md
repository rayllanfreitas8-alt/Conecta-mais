# Conecta+

Aplicativo Android de rede social em português brasileiro para descobrir pessoas, fazer amizades e conversar.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm --filter @workspace/conecta-plus run dev` — run the Expo mobile app
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` for the shared API; `EXPO_PUBLIC_SUPABASE_URL` and `EXPO_PUBLIC_SUPABASE_PUBLISHABLE_KEY` for Conecta+ mobile

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- Mobile: Expo, React Native, Expo Router
- Auth/database/realtime: Supabase Auth and PostgreSQL with RLS
- API: Express 5 (shared workspace service)
- DB: PostgreSQL + Drizzle ORM (shared API package)
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/conecta-plus/app/` — login/cadastro, navegação e telas do app
- `artifacts/conecta-plus/context/AuthContext.tsx` — sessão, autenticação e perfil
- `artifacts/conecta-plus/lib/social.ts` — solicitações, amizades, conversas e mensagens
- `artifacts/conecta-plus/supabase/schema.sql` — tabelas, funções e políticas RLS
- `artifacts/conecta-plus/SUPABASE.md` — instruções para conectar um projeto Supabase
- `artifacts/conecta-plus/constants/colors.ts` — identidade visual do app

## Architecture decisions

- O app se conecta ao Supabase diretamente com a chave publicável; a segurança por usuário fica no RLS do banco.
- Nunca usar a chave `service_role` no aplicativo.
- O projeto Netlify informado pelo usuário é independente e não deve ser alterado por este app.
- Não incluir fluxos de pagamento nesta etapa.

## Product

- Áreas principais: Descobrir, Conversas, Meu perfil e Configurações.
- O cadastro cria um perfil associado ao usuário autenticado.
- Mensagens são privadas para os membros da conversa e usam Supabase Realtime.

## User preferences

_Populate as you build — explicit user instructions worth remembering across sessions._

## Gotchas

_Populate as you build — sharp edges, "always run X before Y" rules._

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
