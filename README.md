# Tutorial de minteo de NFTs en la blockchain de Solana

## Fuentes: 

CMv2: 

https://www.youtube.com/watch?v=-nUtsdxZvqM

https://www.youtube.com/watch?v=KJOWBc0V4sE&t=4265

Metaplex Docs:

https://docs.metaplex.com/candy-machine-v2/getting-started

<br>
<br>

## Requisitos para mintear NFTs en Solana 
<br>

1) Instalar NVM for Windows (https://github.com/coreybutler/nvm-windows) solo porque en los videos utiliza Hashlips que es un complemento para generar NFTs de manera algorítmica. Para el uso de Metaplex y Candymachine se necesita la version 16.14.2 . <br><br>Comandos nvm (abrir como administrador):<br><br>
`nvm ls` lista las versiones de node instaladas<br>
`nvm list available` lista las versiones disponibles para instalar<br>
`nvm list 14.18.1` instala la version <br>
`nvm use` -> usa esa version<br>
`nvm current` tira la version actual de node<br><br>


2) Instalar nvm, git, node, yarn, ts-node. Chequear versiones (por las dudas instale las mismas que en la documentacion):<br>

```
nvm version
// 1.1.9
git version 
//output: git version 2.32.0 

node --version 
//output: v16.14.2 

yarn --version 
//output: 1.22.18 (solo anda con CMD, no con gitbash)

ts-node --version 
//output: v10.5.0 (en la doc pide la 10.4.0, anduvo igualmente)
```
<br>


<mark>Ojo con APPLE CHIP M1 https://docs.metaplex.com/candy-machine-v2/getting-started</mark><br><br>

## Solana Wallet

https://docs.solana.com/cli/install-solana-cli-tools
<br><br>

3) Abrir CMD con permisos de administrador y descargar el instalador de Solana en directorio temporal: <br>`curl https://release.solana.com/v1.9.9/solana-install-init-x86_64-pc-windows-msvc.exe --output C:\solana-install-tmp\solana-install-init.exe --create-dirs`<br><br>
Instalar con:<br>
`C:\solana-install-tmp\solana-install-init.exe v1.9.9`<br><br>
Chequear instalación con:
```
solana --version
//output: solana-cli 1.9.1
```
Instalar actualizacioes con:
`solana-install update`

## Metaplex 
<br>

4) Clonar metaplex:<br> `git clone https://github.com/metaplex-foundation/metaplex.git ./metaplex`

5) Instalar dependencias desde fuera del repo con:<br> `yarn install --cwd .\metaplex\js\` 
<br><br>
Si no funciona se le puede agregar `--network-timeout 500000`<br><br>
Tarda un monton. (puede ser porque el antivirus chequea todos los archivos. en el sition de yarn dice: "Please whitelist your project folder and the Yarn cache directory (%LocalAppData%\Yarn) in your antivirus software, otherwise installing packages will be significantly slower as every single file will be scanned as it’s written to disk.")<br><br>
Chequear que estemos usando la "candy-machine-v2-cli.ts" con:

```
ts-node .\metaplex\jspackages\cli\src\candy-machine-v2-cli.ts --version
//output: 0.0.2
```
<br>
6) Crear una wallet con:<br>

`solana-keygen new --outfile ./.config/solana/devnet.json`<br> ó crea una wallet cuya clave publica empieza con DEV <br>`solana-keygen grind --starts-with DEV:1`<br><br>


7) Hacer que sea el keypair por default con:<br> `solana config set --keypair ./.config/solana/nombredearchivo.json`<br><br>

8) Setear la network a devnet:<br> `solana config set --url https://metaplex.devnet.rpcpool.com/`<br><br>

Chequear configuracion con<br> `solana config get` 

Debería dar algo asi:
```
Config File: ~/.config/solana/cli/config.yml
RPC URL: https://metaplex.devnet.rpcpool.com/
WebSocket URL: wss://metaplex.devnet.rpcpool.com/ (computed)
Keypair Path: ~/.config/solana/devnet.json
Commitment: confirmed
```

9) Fondear la billetera con:<br>
`solana airdrop 1`<br><br>
Si no funciona podemos ir a [SolFaucet](https://solfaucet.com/)<br>
Para averiguar la direccion publica colocar:<br> `solana address`

10) Ir a phantom wallet para agregar la nueva billetera a la billetera previamente creada. "Añadir/vincular billetera". Importar clave privada. Pegar el contenido del archivo ubicado en "./.config/solana/nombredelarchivo.json" y agregar. Luego ir al simbolo de configuracion (ruedita, abajo a la derecha) y cambiar la red a devnet. Confirmar que tengamos 1 sol.<br><br>

## Configuracion mínima de METAPLEX (config.json)

https://docs.metaplex.com/candy-machine-v2/configuration
<br><br>
**Siempre chequear la estructura de la metadata y la configuracion de la CM en la documentacion**
<br><br>

11) Crear un archivo config.json colocarlo en la carpeta de metaplex. Ahi va la configuracion de la CM. La configuracion minima es asi:<br><br>

```
{
  "price": 0.01,
  "number": 2,
  "gatekeeper": null,
  "solTreasuryAccount": "",
  "splTokenAccount": null,
  "splToken": null,
  "goLiveDate": "25 Dec 2021 00:00:00 GMT",
  "endSettings": null,
  "whitelistMintSettings": null,
  "hiddenSettings": null,
  "storage": "arweave-sol",
  "ipfsInfuraProjectId": null,
  "ipfsInfuraSecret": null,
  "awsS3Bucket": null,
  "nftStorageKey": null,
  "noRetainAuthority": false,
  "noMutable": false
}
```
12) Generar un .json con la metadata de cada .png, empezando desde el numero 0 como nombre de archivo. <br><br>
La estructura es:
```
{
  "name": "",
  "symbol": "",
  "image": "0.jpg", //En image y uri debe tener el mismo valor
  "properties": {
    "files": [
      {
      "uri": "0.jpg", 
      "type": "image/jpg"
      }
      ],
    "category": "image",
    "creators": [{
       "address": "",
       "share": 100
       }]    
},
  "description": "",
  "seller_fee_basis_points": 500,  
  "attributes": [
      {
        "trait_type": "", 
        "value": ""
      },      
  ],  
  "collection": {
    "name": "",  //Esto sale en la preview en phantom
    "family": ""
    }
}
```
13) Colocar las foto y los archivos .json en una carpeta assets dentro de metaplex.<br><br>




## Deploy to CandyMachine <br><br>

14) Antes de subir los nfts, chequear que este bien la metadata con:<br>
`ts-node .\packages\cli\src\candy-machine-v2-cli.ts verify_assets ..\assets`<br><br>
Si sale bien solo chequear y no devuelve error

15) Para subir el nft a la candy machine:<br> `ts-node .\packages\cli\src\candy-machine-v2-cli.ts upload -e devnet -k ..\..\wallet.json -cp ..\config.json -c cache ..\assets`<br><br>
Opciones: <br><br>
-e : devnet /mainnet-beta, <br>
-k :  ..\..\wallet.json, <br>
-cp : ..\config.json,<br>
-c : cache file suffix,<br>
argument : ..\assets<br><br>
Debería dar algo asi para continuar:
```
wallet public key: aasdasd
WARNING: The "arweave" storage option will be going away soon. Please migrate to arweave-bundle or arweave-sol for mainnet.

Beginning the upload for 1 (img+json) pairs
started at: 1646076173369
initializing candy machine
initialized config for a candy machine with publickey: 
asdasdag
Uploading Size 1 { mediaExt: '.jpg', index: '0' }
Processing asset: 0
Writing indices 0-0
Done. Successful = true.
ended at: 2022-02-28T19:23:46.745Z. time taken: 00:00:53
```


16) Verificar con:<br> `ts-node .\packages\cli\src\candy-machine-v2-cli.ts verify_upload -e devnet -k ..\..\wallet.json -c cache`<br>
Debería dar algo asi para poder continuar: 
```
wallet public key: asdasd
Key size 1
Looking at key  0
uploaded (1) out of (1)
ready to deploy!
```

17) Mintear el token con:<br> `ts-node .\packages\cli\src\candy-machine-v2-cli.ts mint_one_token -e devnet -k .\..\wallet.json -c cache`><br><br>
Se puede usar también<br> `ts-node candy-machine-v2-cli.ts mint_multiple_tokens -c cacheName -k ..\wallet.json -n 5`.<br>
Debería dar:
```
wallet public key: asdazdfgasrtb
No instructions provided
No instructions provided
mint_one_token finished q4A6zbRBv3QVLjnmPGA6ho1tLXsmuCDPXXbZsdfvsdfgsdfgdsfg
```
<br>

## Sign NFTs

<br>

- Primero setear la cuenta creadora con<br> `solana config set -k .\wallet.json`
- Luego:<br>`ts-node .\packages\cli\src\candy-machine-v2-cli.ts sign_all -e devnet -k ..\..\wallet.json -c cacheName`

<br>

## Withdraw rent

<br>

- `ts-node .\packages\cli\src\candy-machine-v2-cli.ts withdraw candyMachineID -e devnet -k ..\..\wallet.json`<br><br>

## Burn Token

<br>

- `spl-token burn -v TokenAccount 1` <br>Hay que poner la direccion de la TOKEN ACCOUNT, no la del mint (token en sí), tampoco la de la cuenta que holdea el token address
<br><br>
Para sacar estos datos: `spl-token account -v`
<br><br>

## Close account

<br>

- `spl-token close -v MintAccount` (Token)<br><br>

## Hide and reveal (hiddenSettings)

<br>

Fuente: https://www.youtube.com/watch?v=KJOWBc0V4sE&t=2000s

Se pueden usar para minteos grandes donde no subimos todos los NFT al mismo momento que creamos la CM y el archivo ".cache".
En nuestro caso lo usamos para generar el archivo ".cache", para subir nuestros assets a Arweave sin subirlos a la cadena de bloques.

URI:
No es el link a la imagen sino a la metadata que contiene la imagen.
Stractors dice que para obtener el URI hay que primero deployar una candymachine con un solo asset. Así obtenemos el link de Arweave. Luego hacemos withdraw de la CM con lo cual queda obsoleta.

HASH:
Es un medio para comprobar que no estemos manipulando el archivo .cache . 
Primero se deployea la CM con los assets que queremos reemplazar y con un hash arbitrario de 32 caracteres.

Luego antes de ejecutar el comando  modificamos el archivo de configuracion y ponemos el cache que obtuvimos del deploy. Antes pasarlo por un SHA256 ENCODER.

Antes de actualizarla podes copiar el contenido del archivo .cache y ponerlo en un codificador SHA256 y el resultado ponerlo en el campo HASH del archivo de configuracion.

Luego actualizas con update_nfts_from_existing_cache_file 

De este manera los compradores del NFT que obtendran los valores actualizados pueden comprobar si se uso  exactamente ese archivo .cache y no fue manipulado.

Luego de hacer el deploy si utilizamos hiddenSettings y corremos el comando verify_upload fallará ya que nuestros tokens no estan en la cadena de bloques, enteonces el resultado sera "not all nfts checked out"

- Bajar el repo https://github.com/MyNameisLeon/metaplex/tree/patch-1

- En metaplex\js ejecutar: `yarn install` 

- Subir un NFT con la imagen que queremos que sea la de todos los token a ocultar. No mintear. Withdrawear la CandyMachine.

- Guardar la URI del campo de metadata.

- Deployar otra CM con los NFTS verdaderosç agregando la seccion de hiddenSettings:

<br>

```
 "hiddenSettings": {
    "name":"Roman in the Sky ",
    "uri":"https://arweave.net/hQwRKzZXvd7YpZhDteoqeaufB_79YBHfCypUiPoDIJw",
    "hash":"euguachooalsdkaldfisdkdfkhbuhasd"
},
```

<br>

- Colocar en uri el link guardado previamente de la metadata (no el de la imagen)

- Mintear todos los token e ir a la carpeta cache y crear dos archivos uno "devnet-before.json" y otro "devnet-after.json"<br><br>

En before: 

- Reemplazar el campo link por el valor guardado de la metadata previamente.
- Cambiar el campo name por el colocado previamente en hiddenSettings ( 'nombre' + # )

<br>

- Ejecutar el comando `ts-node candy-machine-v2-cli.ts update_existing_nfts_from_latest_cache_file -e devnet -nc after -c before -k ..\wallet.json 5`

- Ahora debería haberse reemplazado la imagen por la nueva<br><br>

## Actualizar CandyMachine
<br>

`ts-node ./metaplex/js/packages/cli/src/candy-machine-v2-cli.ts update_candy_machine -e devnet -k <WALLET_KEYPAIR> -cp ./metaplex/config.json -c cache`
<br><br>
<mark>OJO en cache va el cache ANTERIOR! </mark>





