mint multiple tokens:
ts-node candy-machine-v2-cli.ts mint_multiple_tokens -c after --keypair .\fgh.json -n 5

update from cache:
ts-node candy-machine-v2-cli.ts update_existing_nfts_from_latest_cache_file -e devnet -nc after -c before -k .\fgh.json 5

withdraw:
ts-node candy-machine-v2-cli.ts withdraw -e devnet -c after -k .\CANDY_ID

upload:
ts-node candy-machine-v2-cli.ts upload -e devnet -k ..\..\..\..\..\asdf.json -cp .\config.json -c cache .\metaplex\assets

show:
ts-node candy-machine-v2-cli.ts show -e devnet -k .\DEVyknGYJNVW7FAraJ1c1zizPqfAcSKahZZYkPPSBhid.json -c 

close:
spl-token close -v 6nwxvp6PK9f729xDMagKmSh7m827Wfbw1vZqALyLX3CW




