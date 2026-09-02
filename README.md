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
