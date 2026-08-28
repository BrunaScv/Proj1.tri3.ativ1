# Proj1.tri3.ativ1

bun -v
bun index.ts

###index.ts

const srv = bun.server ({
     port:3000,
     routes: {
          "/teste":{ 
          GET () => new Response("Brunaa_GET"),
          PUT () => new Response("Brunaa_PUT"),
          DELETE () =>  new Response("Brunaa_DELETE"),
          POST () =>  new Response("Brunaa_POST"),
          
     }
}
})

  Console.log(`Rodando no pc ${srv.url}`)
