# Proj1.tri3.ativ1

bun -v
bun index.ts

index.ts

bun.server ({
     port:3000,
     routes: {
          "/teste": () => new Response("Bingo!")
     }
})

  
