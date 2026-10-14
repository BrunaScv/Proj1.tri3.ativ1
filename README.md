# Proj1.tri3.ativ1

bun -v
bun index.ts

###index.ts

const srv = bun.server ({
     port:3000,
     routes: {
          "/teste":{ 
          GET () => 
            {const url = new URL(req.url)
            const seacrh = url.searchParams
            const nome = seacrh.get("nome")
            console.log(nome)
            return new Response("Brunaa_GET")
             new Response("Brunaa_GET")},
          POST async (req) => 
            const body = await req.body.text()
          console.log(body)
             new Response("Brunaa_POST"),
          
     },
     PUT () => new Response("Brunaa_PUT"),
       DELETE () =>  new Response("Brunaa_DELETE"),
}
})

  Console.log(`Rodando no pc ${srv.url}`)




<!DOCTYPE html>
<html lang='pt-BR'>

<head>
    <meta charset='utf-8'>
    <title>Exemplo</title>
</head>

<body>
    <ul></ul>

    <input type="text" id="nome">
    <button id="bt-cadastro">cadastrar</button>

    <script>
        const lista = document.querySelector("ul")
        const inpNome = document.querySelector("#nome")
        const btCadastro = document.querySelector("#bt-cadastro")

        async function init() {
            const response = await fetch("/cliente")
            const data = await response.json()
            data.forEach(({ nome }) => lista.innerHTML += `<li>${nome}</li>`)
        }

        btCadastro.addEventListener('click', async (ev) => {
            const nome = inpNome.value
            const response = await fetch("/cliente", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ nome })
            })
            inpNome.value = ""
            lista.innerHTML += `<li>${nome}</li>`
        })

        init()
    </script>

</body>

</html>


import { Database } from "bun:sqlite";

const db = new Database("database.sqlite")

db.exec(`
    CREATE TABLE IF NOT EXISTS user (
        id              INTEGER PRIMARY KEY AUTOINCREMENT,
        username        TEXT NOT NULL UNIQUE,
        password_hash   TEXT NOT NULL
    );
`);

export { db }
export default db


import frontend from "./index.html"
import db from "./db.ts"

const srv = Bun.serve({
    port: 3000,
    routes: {
        "/": frontend,

        "/user": {
            POST: async (req) => {
                const body = await req.body?.json()
                const query = db.query(`
                    INSERT INTO user(username, password_hash)
                    VALUES(:username, :password_hash)
                `)
                const data = query.run({
                    ":username": body.username,
                    ":password_hash": body.password
                })
                return Response.json(data)
            },
        }
    },
})

console.log(`Server running on ${srv.url}`)
