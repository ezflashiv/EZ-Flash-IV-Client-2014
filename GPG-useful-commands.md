`gpg --gen-key` - generate new private/public keys pair  
`gpg --list-keys` - see all keys in your ring

`gpg --import public-key.asc` - import public key to your ring  
`gpg --export -a "Name" > public-key.asc` - export public key to a file

`gpg --import private-key.asc` - import private key to your ring  
`gpg --export-secret-key -a "Name" > private-key.asc` - export private key to a file

`gpg --delete-key "Name"` - remove public key from your ring  
`gpg --delete-secret-key "Name"` - remove private key from your ring  

`gpg --encrypt --recipient "Name" ./passwords` - encrypt file with the key  
`gpg --output ./passwords --decrypt ./passwords.gpg` - decrypt file

`gpg --armor --detach-sign ./file` - create a detached signature for a file  
`gpg --verify ./public-key.asc ./file` - verify signature of file