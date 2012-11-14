`gpg --gen-key` - generate new private/public keys pair  
`gpg --list-keys` - list all public keys in your ring  
`gpg --list-secret-keys` - list all private keys in your ring

`gpg --import public-key.asc` - import public key to your ring  
`gpg --export -a "Name" > public-key.gpg` - export public key to a file

`gpg --import private-key.asc` - import private key to your ring  
`gpg --export-secret-key -a "Name" > private-key.gpg` - export private key to a file

`gpg --delete-key "Name"` - remove public key from your ring  
`gpg --delete-secret-key "Name"` - remove private key from your ring  

`gpg --edit-key "Name"` - edit key's attributes

`gpg -e -u "Sender Name" -r "Recipient Name" ./passwords` - encrypt file with the key  

`gpg --output ./passwords --decrypt ./passwords.gpg` - decrypt file

`gpg --armor --detach-sign ./file` - create a detached signature for a file  
`gpg --verify ./public-key.asc ./file` - verify signature of file