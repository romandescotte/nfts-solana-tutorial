## CandyMachine commands
<br>

- mint multiple tokens:<br>
`ts-node candy-machine-v2-cli.ts mint_multiple_tokens -c after --keypair .\wallet.json -n 5`

<br>

- update from cache:<br>
`ts-node candy-machine-v2-cli.ts update_existing_nfts_from_latest_cache_file -e devnet -nc after -c before -k .\wallet.json 5`

<br>

- withdraw:<br>
`ts-node candy-machine-v2-cli.ts withdraw -e devnet -c after -k .\CANDY_ID`

<br>

- upload:<br>
`ts-node candy-machine-v2-cli.ts upload -e devnet -k ..\..\..\..\..\wallet.json -cp .\config.json -c cache .\metaplex\assets`

<br>

- show:<br>
`ts-node candy-machine-v2-cli.ts show -e devnet -k .\wallet.json -c `

<br>

## spl-token commands

- close:<br>
`spl-token close -v 6nwxvp6PK9f729xDMagKmSh7m827Wfbw1vZqALyLX3CW`




