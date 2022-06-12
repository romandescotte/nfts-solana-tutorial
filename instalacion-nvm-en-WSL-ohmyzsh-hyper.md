Instalar segun instrucciones de 

https://github.com/nvm-sh/nvm#uninstalling--removal (linux y mac) o 
https://github.com/coreybutler/nvm-windows (windows)


En WLS instale la de linux y agregue esta linea a ~/.zshrc y tambiena  a ~/.bashrc:

export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm


Uninstall:

Manual Uninstall
To remove nvm manually, execute the following:

$ rm -rf "$NVM_DIR"
Edit ~/.bashrc (or other shell resource config) and remove the lines below:

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion