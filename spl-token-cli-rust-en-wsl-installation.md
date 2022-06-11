Instale rust en WSL con:

curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

Luego al intentar instalar spl-token-cli me tiro el error de "error: linker `cc` not found". Entonces, tuve que isntalar C++ build tools:

sudo apt install build-essential


error: "Most likely, you need to install a pkg-config package for your OS.
  Try `apt install pkg-config`, or `yum install pkg-config`,
  or `pkg install pkg-config` depending on your distribution."

sudo apt install pkg-config

sudo apt install libssl-dev

sudo apt install libudev-dev

Luego de la instalacion me dejo instalar spl-token-cli



Solana-cli
agregar esta linea en ~/.zshrc
export PATH="/home/sk8mumy/.local/share/solana/install/active_release/bin:$PATH"

