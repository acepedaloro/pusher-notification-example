
## npm package
```
npm install pusher-js
```

## step 1

```
<script src="./node_modules/pusher-js/dist/web/pusher.min.js"></script>  

// reemplazar por la llave pusher de producction
const pusherKey = ''
    
const pusher = new Pusher(pusherKey, {
    cluster: 'us2'
})
```

## step 2
```
//se reemplaza por el id del post que tenga el usuario
const postId = '5feca65a9c159f7b395fcee2'

//se subscribe al canal privado del post para los eventos
- post-shared
- post-comment
- post-liked

const postTrackingChannel = pusher.subscribe(`post-tracking-${postId}`)

//se subscribe al canal publico challenges-tracking para los eventos
- challenge-created

const challengeTrackingChannel = pusher.subscribe('challenges-tracking')
```

## step 3
```

//se observan eventos de cada canal
postTrackingChannel.bind('post-shared', (data) => {      
    console.log(JSON.stringify(data))
    /*
    ejemplo de data recibida
    {
        "data":{
            "post":"5feca65a9c159f7b395fcee2",
            "user":{
                "id":"6036cfbc8c5bf449437fd382",
                "name":"alejandroklaaa cepeda"
            },
            "challenge":{
                "id":"5feca3ee8f79032af07e97a2",
                "name":"#GanaLoroManiaX2X",
                "description":"gana 10 millon de pesos en bonos con #loro"
            }
        }
    }
    */
})

postTrackingChannel.bind('post-comment', (data) => {       
    console.log(JSON.stringify(data))           
    /*
    ejemplo de data recibida
    {
        "data":{
            "post":"5feca65a9c159f7b395fcee2",
            "comment":"test de comentario",
            "user":{
                "id":"6036cfbc8c5bf449437fd382",
                "name":"alejandroklaaa cepeda"
            },
            "challenge":{
                "id":"5feca3ee8f79032af07e97a2",
                "name":"#GanaLoroManiaX2X",
                "description":"gana 10 millon de pesos en bonos con #loro"
            }
        }
    }
    */
})

postTrackingChannel.bind('post-liked', (data) => {                

    console.log(JSON.stringify(data))
    /*
    ejemplo de data recibida
    {
        "data":{
            "post":"5feca65a9c159f7b395fcee2","
            user":{
                "id":"6036cfbc8c5bf449437fd382",
                "name":"alejandroklaaa cepeda"
            },
            "challenge":{
                "id":"5feca3ee8f79032af07e97a2",
                "name":"#GanaLoroManiaX2X",
                "description":"gana 10 millon de pesos en bonos con #loro"
            }
        }
    }
    */
})

//se observa el evento challenge-created
challengeTrackingChannel.bind('challenge-created', (data) => {          
    console.log(JSON.stringify(data))
    /*
    ejemplo de data recibida
    {
    "data":{          
        "challenge":{
        "id":"5feca3ee8f79032af07e97a2",
        "name":"#GanaLoroManiaX2X",
        "description":"gana 10 millon de pesos en bonos con #loro"
        }
    }
    }    
    */
})

```