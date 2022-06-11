# Actualizar la metadata de Collection NFT

## Instalar metaboss
<br>
`bash <(curl -sSf https://raw.githubusercontent.com/samuelvanderwaal/metaboss/main/scripts/install.sh)`
<br><br>
fuentes: <br>
https://metaboss.rs/overview.html<br>
https://github.com/samuelvanderwaal/metaboss<br>
https://stackoverflow.com/questions/72499758/how-do-i-change-the-name-of-a-solana-collection-prior-to-minting/72500455#72500455

<br><br>

`metaboss update data --keypair <KEY_PAIR> --account <COLLECTION_MINT_ADDRESS> --new-data-file <NEW_JSON_FILE>`

--account: chequear en solscan que diga NFT name: Collection NFT (symbol). Luego de la creacion de la candy machine arroja el dato Collection Mint Address.
<br><br>
El archivo .json debe mantener esta estructura:<br>
```
{
  "name": "BlackNose Tribute Series",
  "symbol": "BCKN",
  "uri": "",
  "sellerFeeBasisPoints": 0,
  "creators": [
    {
      "address": "<ADDRESS>", //billetera creadora de la Candy
      "verified": 1,
      "share": 100
    }
  ]
}
```

Cada campo debe mantener la misma información original, de lo contrario se va a actualizar con lo que diga el .json .

<mark>Nuevamente, la data se puede sacar de solscan buscando la collection_mint_address arrojada en la creacion de la CandyMachine</mark>

(Note: The on-chain Data struct is different than the external metadata stored at the link in the uri field so make you understand the difference before running this command)<br><br>


## Actualizar imagen de colección 
<br>
Tengo que primero subir un archivo a arweave (creo una Candy) sin mintearlo, luego withdrawear la Candy (igual que si quisiera usar Hide and Reveal). <br>Luego utilizo el dato del campo URI y lo coloco en el .json . (no es el URI de la imagen, sino de la metadata)