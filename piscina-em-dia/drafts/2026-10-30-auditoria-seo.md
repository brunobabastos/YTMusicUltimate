# Auditoria SEO local — piscinaemdia.pt

*Data: 2026-10-30 · Âmbito: site completo (uma página) + SEO local · Rascunho para aprovação; nada foi alterado no site.*

## Resumo

A base técnica está bem feita: HTTPS, `lang="pt-PT"`, canonical, robots.txt e sitemap corretos, título bom, dados estruturados `LocalBusiness` com telefone, zona e serviços, e o site funciona bem no telemóvel.

O que limita o SEO local não é técnico. É falta de **páginas**, de **presença no Google Maps** e de **sinais de confiança**:

1. **O site tem uma única página.** Só consegue competir por "manutenção de piscinas Leiria". Pesquisas como "piscina verde", "invernagem" ou "manutenção de piscinas Marinha Grande" não têm uma página que lhes responda.
2. **Perfil de Empresa no Google (Google Maps).** É o fator n.º 1 para aparecer no mapa, e não sei se existe nem como está. → *pergunta para si*
3. **Não há política de privacidade nem ligação ao Livro de Reclamações Eletrónico.** O formulário recolhe nome e telefone, o que pede uma política de privacidade (RGPD). Em Portugal, quem presta serviços a consumidores em geral tem de ter a ligação ao Livro de Reclamações no site. → *confirme com o seu contabilista ou jurista*
4. **O telefone só aparece por JavaScript.** No código da página os elementos de contacto estão vazios. Se o script falhar, o número não aparece, e o Google lê o contacto com menos fiabilidade.
5. **Endereços que não existem devolvem a página inicial em vez de um erro 404.**

## O que não consegui verificar

- **Indexação e tráfego:** não tenho acesso ao Google Search Console.
- **Velocidade (Core Web Vitals):** este ambiente bloqueia as bibliotecas externas do site, por isso a medição não seria fiel. Use o https://pagespeed.web.dev.
- **Redirecionamentos de `http://` e `www.`:** este ambiente só pode aceder a `https://piscinaemdia.pt`.
- **Sites dos concorrentes e resultados do Google:** estão fora do acesso deste ambiente.

## Problemas encontrados

### Técnico

| # | Problema | Impacto | Evidência | Correção |
|---|----------|---------|-----------|----------|
| T1 | Endereços inexistentes devolvem 200 com a página inicial (*soft 404*) | Médio | `/naoexiste-teste` → 200, a mesma página | Configurar o servidor/Cloudflare para responder 404 com uma página de erro simples |
| T2 | Contactos só existem depois de o JavaScript correr | Médio | `<a data-tel></a>` vazio no código; com a biblioteca Supabase bloqueada, o número não apareceu | Escrever o número diretamente no código (`<a href="tel:+351928310814">+351 928 310 814</a>`) e manter o script como complemento |
| T3 | Toda a página depende do script do Supabase | Baixo | Sem a biblioteca, o script para com o erro "supabase is not defined" | Envolver a criação do cliente Supabase num `try`, para o resto da página funcionar sempre |
| T4 | O sitemap só tem a página inicial | Baixo (por agora) | `sitemap.xml` com 1 URL | Acrescentar cada nova página quando for criada |
| T5 | Os títulos `<h1>` da área de cliente estão no mesmo código da página pública | Baixo | 4 `<h1>` no código (só 1 visível na página pública) | Mudar os da área de cliente para `<h2>`, ou carregá-los só quando são abertos |

### Na página

| # | Problema | Impacto | Evidência | Correção |
|---|----------|---------|-----------|----------|
| P1 | O H1 não tem a pesquisa principal | Médio | H1: "Piscina pronta a usar, semana após semana." | Manter a frase e pôr por cima uma linha curta: "Manutenção de piscinas em Leiria" (ou passar o H1 para essa linha) |
| P2 | A meta description tem 164 caracteres e pode ser cortada | Baixo | Ver o código | Proposta (153): "Manutenção, limpeza e tratamento de piscinas em Leiria, Marinha Grande, Batalha e Pombal. Relatório de cada visita no telemóvel. Peça orçamento." |
| P3 | Pouco texto (~500 palavras), sem perguntas frequentes | Médio | Contagem no código | Acrescentar uma secção "Perguntas frequentes" com perguntas reais dos clientes (ver C2) |
| P4 | Os dados estruturados podem ser mais completos | Baixo | Faltam `sameAs`, horário e `priceRange` | Acrescentar `sameAs` com as ligações ao Perfil de Empresa no Google e às redes sociais, quando existirem. Horário e gama de preços só se confirmar os valores |

### Conteúdo e confiança

| # | Problema | Impacto | Correção |
|---|----------|---------|----------|
| C1 | Não há página por serviço | **Alto** | Criar páginas próprias, cada uma com texto útil e fotos reais: **Recuperação de piscinas verdes**, **Preparação da piscina para o inverno (invernagem)**, **Preparação da piscina para o verão**, **Manutenção para alojamento local** |
| C2 | Não há avaliações nem testemunhos no site | **Alto** | Pedir avaliações no Google aos clientes atuais e mostrar algumas no site, com autorização |
| C3 | Não há informação sobre quem faz o trabalho | Médio | Secção "Quem somos": quem trata das piscinas, há quanto tempo, como trabalham. Só com factos que confirmar |
| C4 | Não há política de privacidade nem Livro de Reclamações | Médio (e legal) | Página de política de privacidade ligada no formulário e no rodapé; ligação ao Livro de Reclamações Eletrónico no rodapé |
| C5 | Não há páginas por localidade | Médio (depois de C1) | Marinha Grande, Batalha e Pombal só valem a pena com conteúdo diferente em cada uma (fotos e casos dessa zona). Páginas iguais com o nome da terra trocado podem prejudicar o site |

## Pesquisas a trabalhar (hipóteses)

Não tenho acesso a ferramentas de volume de pesquisa. A lista abaixo é uma hipótese a confirmar no Search Console quando estiver ligado.

| Pesquisa | Página que deve responder |
|----------|---------------------------|
| manutenção de piscinas Leiria / limpeza de piscinas Leiria | Página inicial |
| piscina verde / recuperar piscina verde Leiria | Recuperação de piscinas verdes |
| invernagem piscina / preparar piscina para o inverno | Preparação para o inverno |
| abrir piscina / preparar piscina para o verão | Preparação para o verão |
| manutenção piscina alojamento local | Alojamento local |
| manutenção de piscinas Marinha Grande / Batalha / Pombal | Páginas por localidade (fase 2) |

## Plano por ordem

**1. Já (rápido, sem custo)**
- Confirmar ou criar o Perfil de Empresa no Google: categoria, zona de serviço, telefone, site, serviços (incluindo as preparações para o inverno e o verão), fotos reais.
- Começar a pedir avaliações no Google aos clientes atuais, com uma mensagem curta no WhatsApp e o link direto.
- Pôr o telefone diretamente no código (T2) e corrigir a meta description (P2).
- Ligar o Google Search Console e submeter o sitemap.

**2. Próximas semanas (alto impacto)**
- Política de privacidade e Livro de Reclamações (C4).
- Linha "Manutenção de piscinas em Leiria" no topo (P1).
- Página de **Preparação para o inverno**: é a época certa agora.
- Página de **Recuperação de piscinas verdes**, a tempo da primavera.

**3. Depois**
- Páginas de preparação para o verão e de alojamento local, perguntas frequentes, "Quem somos".
- Corrigir o erro 404 (T1) e tornar a página independente do Supabase (T3).
- Páginas por localidade, só com conteúdo próprio.
