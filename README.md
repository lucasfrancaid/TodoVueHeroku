# Todo Vue.js estático com deploy no Heroku

## Configurando o app:
Partindo da premissa que o app já está pronto, vamos configurá-lo para subir de maneira estática no Heroku.

Adicione o seguinte arquivo com o nome "static.json" na pasta raíz do projeto:
```json
{
  "root": "dist",
  "clean_urls": true,
  "routes": {
    "/**": "index.html"
  }
}
```

Faça o commit das alterações com Git:
```bash
$ git add . && git commit -m "Heroku config"
```

Crie o build de produçao:
```bash
$ npm run build
```

## Criando o app no Heroku e fazendo o deploy:
Antes de tudo, você deve ter o Heroku instalado globalmente em sua máquina, caso não tenha, instale com:
```bash
$ npm install -g heroku
```

Faça o login e crie o app no Heroku:
```bash
$ heroku login
$ heroku apps:create todovuejs-lucasfranca
```
*OBS: O nome do app deve ser único, pois será usado para gerar o link da aplicação.*

Execute os seguintes comandos para instalar os pacotes de buld do Heroku, eles são essenciais, pois irão garantir que a aplicação seja estática:
```bash
$ heroku buildpacks:add heroku/nodejs
$ heroku buildpacks:add https://github.com/heroku/heroku-buildpack-static
```

Faça um git remote e depois faça o push do repositório no Heroku:
```bash
$ heroku git:remote --app todovuejs-lucasfranca
$ git push heroku master
```

Se tudo ocorreu bem no deploy, a sua aplicação já está no ar 😉.
