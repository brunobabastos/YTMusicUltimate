# Correções rápidas para o site — texto para colar no chat do site

*Rascunho de 2026-10-30, a partir da auditoria SEO. Antes de colar, preencha os campos entre [PARÊNTESES RETOS] na política de privacidade.*

```
Preciso de 6 alterações no site piscinaemdia.pt. Não mexas em mais nada.

1) TELEFONE ESCRITO DIRETAMENTE NO HTML
Hoje os links de contacto estão vazios no HTML e só são preenchidos pelo JavaScript.
- Na secção #contacto, troca <a class="btn escuro" data-tel></a> por:
  <a class="btn escuro" data-tel href="tel:+351928310814">+351 928 310 814</a>
- Nos links data-whats (secção #contacto e barra #barraContacto), acrescenta já no HTML:
  href="https://wa.me/351928310814"
- No botão "Ligar" da barra (#barraLigar), acrescenta no HTML: href="tel:+351928310814"
- No rodapé, por baixo da zona, acrescenta o número como texto com link:
  <a href="tel:+351928310814">+351 928 310 814</a>
O script pode continuar a preencher estes elementos a partir do CONFIG; o resultado tem de ser o mesmo.

2) META DESCRIPTION MAIS CURTA
Troca o conteúdo de <meta name="description"> por:
"Manutenção, limpeza e tratamento de piscinas em Leiria, Marinha Grande, Batalha e Pombal. Relatório de cada visita no telemóvel. Peça orçamento."

3) PESQUISA PRINCIPAL NO TOPO
Por cima do H1 "Piscina pronta a usar, semana após semana.", acrescenta uma linha pequena (estilo de etiqueta/sobretítulo, discreta):
"Manutenção de piscinas em Leiria"
Mantém o H1 como está.

4) A PÁGINA CONTINUA A FUNCIONAR SE O SUPABASE FALHAR
Hoje, se a biblioteca do Supabase não carregar, o script para com "supabase is not defined" e o resto da página deixa de funcionar.
- Envolve a criação do cliente (supabase.createClient(...)) num try/catch. Se falhar, sb fica null e a página pública (preços, calculadora, contactos, mapa) continua a funcionar.
- No formulário de orçamento, se sb for null, mostra: "Não foi possível enviar. Ligue ou envie WhatsApp para +351 928 310 814."
- Os títulos <h1> da área de cliente ("Área de cliente", "Link sem acesso", "Olá, ...") passam a <h2>, mantendo o mesmo aspeto visual (ajusta o CSS se for preciso). Assim a página pública fica com um só H1.

5) ERRO 404 PARA ENDEREÇOS QUE NÃO EXISTEM
Hoje qualquer endereço (ex.: /qualquer-coisa) devolve a página inicial com código 200.
- Cria um 404.html simples na raiz, com o mesmo cabeçalho e rodapé, o texto "Página não encontrada" e um botão para a página inicial, e <meta name="robots" content="noindex">.
- Se o site estiver no Cloudflare Pages, basta existir o 404.html na raiz. Se estiver noutro alojamento, configura-o para devolver código 404 com essa página.
- A área de cliente usa links com # (ex.: /#/p/<token>), por isso continua a funcionar. Confirma isso depois da alteração.

6) POLÍTICA DE PRIVACIDADE (RGPD)
- Cria uma página privacidade.html, com o mesmo cabeçalho e rodapé do site, com o texto que está no fim desta mensagem.
- No rodapé, acrescenta um link "Política de privacidade" para /privacidade.html.
- No formulário de orçamento, por baixo do botão "Pedir orçamento", acrescenta em letra pequena:
  "Usamos os seus dados só para responder ao pedido. Ver a <a href="/privacidade.html">política de privacidade</a>."
- Acrescenta https://piscinaemdia.pt/privacidade.html ao sitemap.xml.

Depois de alterar, confirma:
- com o JavaScript desligado, o número de telefone aparece e os links tel: e wa.me funcionam;
- https://piscinaemdia.pt/qualquer-coisa devolve código 404;
- https://piscinaemdia.pt/#/entrar e um link de cliente /#/p/... continuam a abrir a área de cliente;
- a página pública só tem um <h1>;
- o resto da página, a calculadora e o formulário funcionam como antes.

--- TEXTO DA PÁGINA privacidade.html ---

Política de privacidade

Última atualização: [DATA]

Quem é o responsável pelos dados
[NOME DO RESPONSÁVEL OU DA EMPRESA], NIF [NIF], [MORADA OU LOCALIDADE].
Contacto para questões de privacidade: [EMAIL] ou +351 928 310 814.

Que dados recolhemos
- Pedido de orçamento: nome, telefone e localidade, e fotos da piscina se as enviar.
- Clientes: dados da morada da piscina, registos e fotos das visitas, produtos usados e faturas, que ficam disponíveis na área de cliente.

Para que usamos os dados
- Responder ao seu pedido de orçamento.
- Prestar o serviço de manutenção e manter o registo das visitas na sua área de cliente.
- Cumprir obrigações legais, como a faturação.
Não usamos os seus dados para publicidade nem os vendemos a terceiros.

Fundamento
Diligências pré-contratuais a seu pedido (orçamento), execução do contrato (clientes) e cumprimento de obrigações legais (faturação).

Durante quanto tempo guardamos os dados
- Pedidos de orçamento que não deram origem a serviço: [PRAZO, por exemplo 12 meses].
- Clientes: enquanto durar o serviço e, depois disso, pelos prazos exigidos por lei, por exemplo para documentos de faturação.

Quem trata os dados por nós
Usamos prestadores de serviços técnicos para alojar o site e guardar os dados: Supabase (base de dados e fotos) e Cloudflare (alojamento e estatísticas de visitas). O site carrega também tipos de letra do Google Fonts.

Os seus direitos
Pode pedir acesso, correção ou eliminação dos seus dados, opor-se ao seu tratamento ou pedir a sua portabilidade, através do contacto acima. Pode também apresentar reclamação à Comissão Nacional de Proteção de Dados (www.cnpd.pt).
```
