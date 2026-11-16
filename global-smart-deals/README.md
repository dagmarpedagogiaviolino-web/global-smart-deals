# Global Smart Deals

Site estático multilíngue (português, inglês e espanhol) para curadoria e divulgação de produtos por afiliados. Preparado para hospedagem estática no Cloudflare Pages.

## O que está incluído

- Página inicial responsiva, catálogo com busca e filtros por categoria/moeda.
- Cartões de produto e janela de detalhes.
- Seletor de idioma com preferência salva no navegador.
- Artigos demonstrativos, contato por `mailto:` configurável e aviso de cookies.
- Páginas legais iniciais (modelos que precisam ser revisados e personalizados).
- SEO básico, Open Graph, JSON-LD, `robots.txt`, `sitemap.xml`, favicon e manifest.
- Dados de produtos e artigos separados do código.

## Importante antes de publicar

1. Os três produtos iniciais são **demonstrações**, não ofertas reais.
2. Não há preço, avaliação, depoimento ou link de afiliado inventado.
3. Edite `data/products.json` e substitua as demonstrações por ofertas reais para as quais você tenha aprovação.
4. Atualize `assets/config.js` com um e-mail real e seus perfis sociais.
5. Substitua `SEU-PROJETO.pages.dev` em `robots.txt` e `sitemap.xml` pelo endereço definitivo.
6. Preencha os dados do operador nas páginas legais e obtenha revisão jurídica/privacidade adequada aos países em que atuar.
7. O formulário de newsletter é apenas uma interface demonstrativa: não coleta nem envia e-mails. Para ativá-lo, será necessário conectar um provedor e implementar consentimento e política correspondentes.
8. A escolha de cookies está implementada para a experiência inicial, mas não é uma CMP completa. Não instale analytics, pixels ou publicidade sem implementar consentimento apropriado.
9. Nenhum botão simula checkout. O visitante só poderá ir ao anunciante quando um link HTTPS válido for configurado.

## Testar localmente

Como os dados são carregados por `fetch`, abra o projeto através de um servidor HTTP local, não diretamente com `file://`.

Com Python 3 instalado, na pasta do projeto:

```bash
python -m http.server 8000
```

Abra `http://localhost:8000`.

## Cadastrar, editar ou remover produtos

Edite `data/products.json`. Cada produto usa esta estrutura:

```json
{
  "id": "identificador-unico",
  "name": {
    "pt": "Nome em português",
    "en": "Name in English",
    "es": "Nombre en español"
  },
  "description": {
    "pt": "Descrição factual em português.",
    "en": "Factual description in English.",
    "es": "Descripción factual en español."
  },
  "category": "software",
  "currency": "USD",
  "price": null,
  "platform": "Nome da plataforma",
  "officialUrl": "https://site-oficial.example/",
  "affiliateUrl": "https://link-de-afiliado-aprovado.example/",
  "language": ["pt", "en", "es"],
  "updated": "2026-11-16",
  "icon": "✦",
  "tone": "tone-lilac",
  "demo": false
}
```

- `id`: identificador único, sem espaços.
- `name` e `description`: textos nos três idiomas.
- `category`: use `software`, `education`, `home` ou `other` (categorias adicionais exigem pequena edição no `assets/app.js`).
- `currency`: `USD` ou `EUR` (ou moeda suportada pelo navegador).
- `price`: número ou `null` quando não houver preço verificado.
- `officialUrl`: URL pública do vendedor.
- `affiliateUrl`: seu link exclusivo, gerado pela plataforma após aprovação.
- `demo`: defina `false` somente para ofertas reais verificadas.

Para editar, altere os campos e salve. Para remover, apague o objeto completo da lista JSON. Mantenha vírgulas válidas entre objetos. Não use links sem autorização ou links de afiliados de outra pessoa.

## Publicar gratuitamente no Cloudflare Pages

1. Crie uma conta em https://dash.cloudflare.com/.
2. Crie um repositório no GitHub e envie todos os arquivos desta pasta para a raiz do repositório.
3. No Cloudflare, abra **Workers & Pages** → **Create application** → **Pages** → conecte ao Git.
4. Selecione o repositório.
5. Para este projeto HTML estático, deixe o comando de build vazio e configure o diretório de saída como `.` (raiz do projeto), conforme a interface atual.
6. Clique em **Save and Deploy**.
7. O Cloudflare fornecerá um subdomínio `*.pages.dev`.
8. Atualize `robots.txt` e `sitemap.xml` com o subdomínio final e envie as alterações ao GitHub.
9. Teste a versão publicada em computador e celular.

A hospedagem estática e o subdomínio fornecido podem ser usados no plano gratuito, sujeitos aos limites e termos atuais da Cloudflare. Um domínio próprio registrado normalmente não é gratuito.

## SEO e Google

- Troque o endereço de exemplo em `sitemap.xml` e `robots.txt`.
- Cadastre o domínio/subdomínio no Google Search Console e envie o sitemap.
- Não há Google Analytics ativo. Se for instalar, configure consentimento, reveja a política e não exponha credenciais.
- Produza análises originais, úteis e verificáveis. Não copie descrições de vendedores.

## Limitações desta versão

- Sem painel administrativo: produtos são geridos editando o JSON e publicando novamente.
- Sem backend, checkout, pagamentos, banco de dados, sistema de comentários ou envio de newsletter.
- O formulário de contato usa o aplicativo de e-mail do visitante quando `contactEmail` é configurado.
- Os textos legais são modelos informativos e não aconselhamento jurídico.
