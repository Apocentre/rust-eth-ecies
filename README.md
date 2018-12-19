```
extern crate eth_ecies;

use eth_ecies::brain;
use eth_ecies::Generator;
use eth_ecies::crypto::ecies;
use std::str::from_utf8;

fn main() {

    let keypair = brain::Brain::new("brain phrase !".to_string()).generate().unwrap();

    let public = keypair.public();
    let secret = keypair.secret();

    let ciphertext = ecies::encrypt(public,b"",b"Text to encrypt").unwrap();

    println!("Cyphertext {:?}",ciphertext);

    let decrypted = ecies::decrypt(secret,b"",&ciphertext).unwrap();

    println!("Decrypted {:?}",from_utf8(&decrypted).unwrap().to_string());
    
}
```
