axios
versión npm estado de construcción cobertura de código descargas npm dependencias de desarrollo

Cliente HTTP basado en promesas para el navegador y node.js

Caracteristicas
Hacer XMLHttpRequests desde el navegador
Realizar solicitudes http desde node.js
Admite la API Promise
Interceptar solicitud y respuesta
Transformar los datos de solicitud y respuesta
Transformaciones automáticas para datos JSON
Soporte del lado del cliente para protegerse contra XSRF
Soporte del navegador
Cromo	Firefox	Safari	Ópera	ES DECIR
Último ✔	Último ✔	Último ✔	Último ✔	8+ ✔
Instalando
Usando bower:

$ bower instalar axios
Usando npm:

$ npm instalar axios
Ejemplo
Realización de una GETsolicitud

// Realizar una solicitud para un usuario con un ID determinado 
axios . get ( '/ user? ID = 12345' ) 
  . luego ( función  ( respuesta )  { 
    consola . registro ( respuesta ) ; 
  } ) 
  . captura ( función  ( respuesta )  { 
    consola . registro ( respuesta ) ; 
  } ) ;

// Opcionalmente, la solicitud anterior también se puede realizar como 
axios . get ( '/ usuario' ,  { 
    params : { 
      ID : 12345 
    } 
  } ) 
  . luego ( función  ( respuesta )  { 
    consola . registro ( respuesta ) ; 
  } ) 
  . captura ( función  ( respuesta )  { 
    consola . registro ( respuesta ) ; 
  } );
Realización de una POSTsolicitud

axios . posterior ( '/ user' ,  { 
    primerNombre : 'Fred' , 
    lastName : 'Picapiedra' 
  } ) 
  . luego ( función  ( respuesta )  { 
    consola . registro ( respuesta ) ; 
  } ) 
  . captura ( función  ( respuesta )  { 
    consola . registro ( respuesta ) ; 
  } ) ;
Realización de múltiples solicitudes simultáneas

function  getUserAccount ( )  { 
  devolver  axios . obtener ( '/ usuario / 12345' ) ; 
}

function  getUserPermissions ( )  { 
  return  axios . get ( '/ usuario / 12345 / permisos' ) ; 
}

axios . all ( [ getUserAccount ( ) ,  getUserPermissions ( ) ] ) 
  . then ( axios . spread ( function  ( acct ,  perms )  { 
    // Ambas solicitudes ahora están completas 
  } ) ) ;
API de axios
Las solicitudes se pueden realizar pasando la configuración relevante a axios.

axios (config)
axios ( { 
  método : 'obtener' , 
  url : '/ usuario / 12345' 
} ) ;
Solicitar alias de métodos
Para mayor comodidad, se han proporcionado alias para todos los métodos de solicitud admitidos.

axios.get (url [, config])
axios.delete (url [, config])
axios.head (url [, config])
axios.post (url [, data [, config]])
axios.put (url [, data [, config]])
axios.patch (url [, data [, config]])
NOTA
Al utilizar los métodos de alias url, methody datapropiedades no necesitan ser especificado en config.

Concurrencia
Funciones de ayuda para tratar solicitudes concurrentes.

axios.all (iterable)
axios.spread (devolución de llamada)
Creando una instancia
Puede crear una nueva instancia de axios con una configuración personalizada.

axios.create ([config])
var  instancia  =  axios . create ( { 
  baseURL : 'https://some-domain.com/api/' , 
  timeout : 1000 , 
  headers : { 'X-Custom-Header' : 'foobar' } 
} ) ;
Métodos de instancia
Los métodos de instancia disponibles se enumeran a continuación. La configuración especificada se fusionará con la configuración de la instancia.

axios # request (config)
axios # get (url [, config])
axios # delete (url [, config])
axios # head (url [, config])
axios # post (url [, data [, config]])
axios # put (url [, data [, config]])
axios # patch (url [, data [, config]])
Solicitar API
Estas son las opciones de configuración disponibles para realizar solicitudes. Solo urlse requiere el. Las solicitudes se establecerán de forma predeterminada en GETsi methodno se especifica.

{ 
  // `url` es la URL del servidor que se utilizará para la 
  URL de solicitud : '/ usuario' ,
  
  // `método` es el método de solicitud que se utilizará al realizar el 
  método de solicitud : 'get' ,  // predeterminado

  // `baseURL` se antepondrá a` url` a menos que `url` sea absoluta. 
  // Puede ser conveniente establecer `baseURL` para una instancia de axios para pasar URL relativas 
  // a los métodos de esa instancia. 
  baseURL : 'https://some-domain.com/api/' ,

  // `transformRequest` permite cambios en los datos de la solicitud antes de que se envíen al servidor 
  // Esto solo es aplicable para los métodos de solicitud 'PUT', 'POST' y 'PATCH' 
  // La última función en la matriz debe devolver un string o un ArrayBuffer 
  transformRequest : [ function  ( data )  { 
    // Haz lo que quieras para transformar los datos

    devolver  datos ; 
  } ] ,

  // `transformResponse` permite que se realicen cambios en los datos de respuesta antes 
  // de que se pasen a / catch 
  transformResponse : [ function  ( data )  { 
    // Haz lo que quieras para transformar los datos

    devolver  datos ; 
  } ] ,

  // `headers` son encabezados personalizados para enviar 
  encabezados : { 'X-Requested-With' : 'XMLHttpRequest' } ,

  // `param` son los parámetros de URL para ser enviados con la solicitud 
  params : { 
    ID : 12345 
  } ,

  // `paramsSerializer` es una función opcional encargada de serializar` params` 
  // (por ejemplo, https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/) 
  paramsSerializer : function ( params )  { 
    return  Qs . stringify ( params ,  { arrayFormat : 'brackets' } ) 
  } ,

  // `data` son los datos que se enviarán como el cuerpo de la solicitud 
  // Solo se aplica a los métodos de solicitud 'PUT', 'POST' y 'PATCH' 
  // Cuando no se establece` transformRequest`, debe ser una cadena, un ArrayBuffer o un 
  dato hash : { 
    firstName : 'Fred' 
  } ,

  // `timeout` especifica el número de milisegundos antes de que se agote el tiempo de espera de la solicitud. 
  // Si la solicitud tarda más de "timeout", la solicitud se cancelará. 
  tiempo de espera : 1000 ,

  // `withCredentials` indica si las solicitudes de control de acceso entre sitios 
  // deben realizarse utilizando credenciales con 
  Credentials : false ,  // default

  // `adapter` permite el manejo personalizado de solicitudes, lo que facilita las pruebas. 
  // Llame a `resolve` o` accept` y proporcione una respuesta válida (consulte los [documentos de respuesta] (# response-api)). 
  adaptador : función  ( resolver ,  rechazar ,  configurar )  { 
    / * ... * / 
  } ,

  // `auth` indica que se debe utilizar la autenticación básica HTTP y proporciona las credenciales. 
  // Esto establecerá un encabezado de `Autorización`, sobrescribiendo cualquier 
  // encabezado personalizado de` Autorización` 
  existente que haya configurado usando `encabezados`. auth : { 
    nombre de usuario : 'janedoe' , 
    contraseña : 's00pers3cret' 
  }

  // `responseType` indica el tipo de datos con los que el servidor responderá 
  // las opciones son 'arraybuffer', 'blob', 'document', 'json', 'text' 
  responseType : ' json ' ,  // predeterminado

  // `xsrfCookieName` es el nombre de la cookie que se utilizará como valor para el token 
  xsrf xsrfCookieName : 'XSRF-TOKEN' ,  // predeterminado

  // `xsrfHeaderName` es el nombre del encabezado http que lleva el valor del token 
  xsrf xsrfHeaderName : 'X-XSRF-TOKEN'  // predeterminado 
}
API de respuesta
La respuesta a una solicitud contiene la siguiente información.

{ 
  // `data` es la respuesta proporcionada por el servidor 
  data : { } ,

  //'Estado` es el código de estado HTTP de la respuesta del servidor 
  de estado : 200 ,

  // `statusText` es el mensaje de estado HTTP de la respuesta del servidor 
  statusText : 'OK' ,

  // `encabezados` los encabezados que el servidor respondió con 
  encabezados : { } ,

  // `config` es la configuración que se proporcionó a` axios` para la 
  configuración de la solicitud : { } 
}
Al usar theno catch, recibirá la respuesta de la siguiente manera:

axios.get('/user/12345')
  .then(function(response) {
    console.log(response.data);
    console.log(response.status);
    console.log(response.statusText);
    console.log(response.headers);
    console.log ( respuesta . config ) ; 
} ) ;
Interceptores
Puede interceptar solicitudes o respuestas antes de que sean manejadas por theno catch.

// Agrega un interceptor de solicitud 
axios . interceptores . solicitud . use ( function  ( config )  { 
    // Haga algo antes de que se envíe la solicitud 
    return  config ; 
  } ,  function  ( error )  { 
    // Haga algo con la solicitud error 
    return  Promise . accept ( error ) ; 
  } ) ;

// Agrega un interceptor de respuesta 
axios . interceptores . respuesta . use ( function  ( respuesta )  { 
    // Hacer algo con los datos de respuesta 
    return  response ; 
  } ,  function  ( error )  { 
    // Hacer algo con la respuesta error 
    return  Promise . Rechazar ( error ) ; 
  } ) ;
Si es posible que necesite eliminar un interceptor más adelante, puede hacerlo.

var  myInterceptor  =  axios . interceptores . solicitud . use ( función  ( )  { /*...*/ } ) ; 
axios . interceptores . solicitud . expulsar ( myInterceptor ) ;
Puede agregar interceptores a una instancia personalizada de axios.

var  instancia  =  axios . crear ( ) ; 
instancia . interceptores . solicitud . use ( función  ( )  { /*...*/ } ) ;
Manejo de errores
axios . obtener ( '/ usuario / 12345' ) 
  . catch ( function  ( response )  { 
    if  ( response  instanceof  Error )  { 
      // Algo sucedió al configurar la solicitud que desencadenó una 
      consola de Error . log ( 'Error' ,  respuesta . mensaje ) ; 
    }  else  { 
      // La solicitud se realizó, pero el servidor respondió con un código de estado 
      // que cae fuera del rango de la 
      consola 2xx . log (respuesta . datos ) ; 
      consola . log ( respuesta . estado ) ; 
      consola . log ( respuesta . encabezados ) ; 
      consola . log ( respuesta . config ) ; 
    } 
  } ) ;
Semver
Hasta que axios llegue a un 1.0lanzamiento, se lanzarán cambios importantes con una nueva versión menor. Por ejemplo 0.5.1, y 0.5.4tendrá la misma API, pero 0.6.0tendrá cambios importantes.

Promesas
axios depende de una implementación nativa de ES6 Promise para ser compatible . Si su entorno no es compatible con ES6 Promises, puede realizar polyfill .

Mecanografiado
axios incluye una definición de TypeScript .

/// <ruta de referencia = "axios.d.ts" /> 
importar  axios  = require ( 'axios' ) ; 
axios . get ( '/ user? ID = 12345' ) ;
Créditos
axios está muy inspirado en el servicio $ http proporcionado en Angular . En última instancia, axios es un esfuerzo por proporcionar un $httpservicio independiente para usar fuera de Angular.

Licencia
MIT
