# TP2 AES et RSA avec Open SSL 
## CRYPTOGRAPHIE NUMERO : 2
---

### I. Chiffrement symétrique AES

#### A. Découverte

  - 1 
      ```
      echo "TESTSECRET1234567" | openssl enc -aes-256-cbc -a -salt
      enter AES-256-CBC encryption password:
      Verifying - enter AES-256-CBC encryption password:
      *** WARNING : deprecated key derivation used.
      Using -iter or -pbkdf2 would be better.
      U2FsdGVkX19rLwla14ZXvffs86yWAoSYY1XXhY3z3hFD1wpqMtQUxnTmpmmmkeui
      ```
  - 2 
      
      OpenSSL transforme le mdp en clé binaire (de 256 bits pour AES 256) avec un algorithme en ajoutant le sel et fait une suele iterations avec une fonction de hachage. Le sel permet d'avoir des déférents clé pour une même mot de passe. Ici la fonction est la EVP_BytesToKey (trés basique qui mouline trés peu le mot de passe)
      Pour renforcer la sécurité on utilise : -pbkdf2 (ajoute milliers d'iterations)

      Exemple de clé hexadécimale générée à partir d'un mot de passe :
      ```
      openssl enc -aes-256-cbc -P -salt
      enter AES-256-CBC encryption password:
      Verifying - enter AES-256-CBC encryption password:
      *** WARNING : deprecated key derivation used.
      Using -iter or -pbkdf2 would be better.
      salt=595E8D941B1F8C03
      key=5B727C28479518CA47E1BFE49C3C1B8CEF8FD37CF66334DC78E952DC2E10B933
      iv =31694E5E33DAB80552B262E2D1EB6B81
      ```
      **salt :** La donnée aléatoire utilisée.

      **key :** La clé réelle. C'est elle qui verrouille mathématiquement vos données.

      **iv :** Le Vecteur d'Initialisation. C'est un second paramètre aléatoire qui assure que si vous chiffrez deux fois la même phrase, le résultat sera différent.

      OpenSSL enregistre toujours le Salt au tout début du fichier chiffré.

  - 3 
      ```
      echo "U2FsdGVkX19rLwla14ZXvffs86yWAoSYY1XXhY3z3hFD1wpqMtQUxnTmpmmmkeui" | openssl enc -aes-256-cbc -d -a -salt
      enter AES-256-CBC decryption password:
      *** WARNING : deprecated key derivation used.
      Using -iter or -pbkdf2 would be better.
      TESTSECRET1234567
      ```

#### B. Transmission  d’un  message  chiffré  à  votre  binôme (passphrase)

  - 1.
    ```
    echo "Fiat 600" | openssl enc -aes-256-cbc -a                                                
    enter AES-256-CBC encryption password:
    Verifying - enter AES-256-CBC encryption password:
    *** WARNING : deprecated key derivation used.
    Using -iter or -pbkdf2 would be better.
    U2FsdGVkX1/+X9C+eJcXo6eV/AQ+Ex8AvI13waI8ht8=
    ```
  - 2. Texte chiffré transféré au binôme : **U2FsdGVkX1/+X9C+eJcXo6eV/AQ+Ex8AvI13waI8ht8=**
     
  - 3. Avec le texte chiffre du binôme et le mdp j’obtiens le déchiffrement suivante :
        ```
        echo "U2FsdGVkX1/5o02L3AiAzg2n3RA1pb2/KQhgrEiT5Lw=" | openssl enc -aes-256-cbc -d -a
        enter AES-256-CBC decryption password:
        *** WARNING : deprecated key derivation used.
        Using -iter or -pbkdf2 would be better.
        Ferrari Enzo
        ```

#### Transmission d’un message chiffré à votre binôme

  - 1 Génération d'une clé de chiffrement et un vecteur d'initialisation (IV) à partir d’une passphrase sans
sel :
      ```
      openssl enc -aes-256-cbc -nosalt -P 
      enter AES-256-CBC encryption password:
      Verifying - enter AES-256-CBC encryption password:
      *** WARNING : deprecated key derivation used.
      Using -iter or -pbkdf2 would be better.
      key=AFBDC8AB49C2AFCA2651BBF189918F13487A68249E2E6830E1803535BFFD24F6
      iv =C03A721D037381CA9DE6F5CC75E8EAE4
      ````
      - Valeurs :
        - **key**=AFBDC8AB49C2AFCA2651BBF189918F13487A68249E2E6830E1803535BFFD24F6
        - **iv**=C03A721D037381CA9DE6F5CC75E8EAE4 
   
  - 2  Chiffrement d'un chanson en utilisant la clé et l’IV générés précédemment
    ```
    echo "L'albatros - Raphaël Imbert, Célia Kameni" | openssl enc -aes-256-cbc -a -K AFBDC8AB49C2AFCA2651BBF189918F13487A68249E2E6830E1803535BFFD24F6 -iv C03A721D037381CA9DE6F5CC75E8EAE4
    ```
  - 3 Résultat envoyé au binôme = xM6k+VhhIGENtdWy1Fw8iRhPkP7s0xsLtTQMMPEPzawvbCuTy6PRgCgmAO2YUD00
  
  - 4 Clé transmise par un autre canal :
    - **key**=AFBDC8AB49C2AFCA2651BBF189918F13487A68249E2E6830E1803535BFFD24F6
    - **iv**=C03A721D037381CA9DE6F5CC75E8EAE4  
      - Déchiffrement du message du binôme avec sa clé et son iv :
          
        ```
        echo "eCR47BQMsqeacNhqojmnw0XrLfSHk1QblW18H7PGB8M=" | openssl enc -aes-256-cbc -d -a -K 84CA006878BF3BAA67524BC5E9B0F0D298232274BA600538CEE4369B1875E3F0 -iv 589E3710FEB7F3421358711CE1770109
        Storia di un grande Amore
        ```  

### II. RSA 

#### A. Génération de la paire de clés RSA 
- `openssl genrsa -out private_key.pem 2048`
- `openssl rsa -in private_key.pem -pubout -out public_key.pem
writing RSA key`



#### B. Chiffrement d’un message 

Utilisation de Base64 Pour manipuler du texte et non des fichiers.
Chiffrement du texte avec la clé publique du binôme :
```
echo "La Playa de los Hippies Cordoba Argentina" | openssl pkeyutl -encrypt -pubin -inkey public_key_hicham.pem | base64 > message_pour_hicham.enc.b64

cat message_pour_hicham.enc.b64 
i0Xw8N6wjVQrVUBs9oAuYZ44BnfR6Y4bypzGcO48V58HoCd3fkw/4+srR6KSCZ6vYX2r0BY7ZXpI
rjkayoZcT8lwQvfDN3UfqNjvvIUhHQ5AgtDgJmQtS7dOJVlv6/Tbj5gWBiPLyuutMo0ojgJ/6LHs
m1GY57LQ8AQTPLJcwuiOMBGs0j2TTAgkPUuJRPZtSyySX20u4ALASALxXx1xfkWPNbUFRYjyrltD
WDHIVjCs5oQv2ZRWhu082ota+N0UklYCt8X1fjuyrabrUJh0NWA6xn44QFaL6Frmb2wO4pFhfkPq
THJFRYWz59bA2yXtlZalM6LSgFanWGWTdj2Bpg==
```


#### C. Échange et déchiffrement 
Déchiffrement du message du binôme avec ma clé PRIVÉE :

```
openssl pkeyutl -decrypt -inkey private_key.pem -in tuvaskiffer_pour_agustin.enc 
Maldives
```

## III. Bonus

- Générer la Clé Symétrique :

```
openssl rand -out ma_cle_aes.bin 32
```
  
- Chiffrement de la clé Symetétrique : 
```

└─$ openssl pkeyutl -encrypt -pubin -inkey public_key_hicham.pem -in ma_cle_aes.bin -out ma_cle_aes.bin.rsa


└─$ openssl pkeyutl -encrypt -pubin -inkey public_key_jimmy.pem -in ma_cle_aes.bin -out ma_cle_aes.bin.rsa
```
  
- Transmission de la clé secrète : OK
  
- Chiffrement des données :
```
openssl enc -aes-256-cbc -salt -pbkdf2 -in gros_fichier.zip -out gros_fichier.enc -kfile ma_cle.key
openssl enc -aes-256-cbc -a -salt -pbkdf2 -iter 100000 -in Plástico_Rubén_Blades.txt -out Plástico_Rubén_Blades.enc
```
  
- Transmission des données chiffrées : OK
  
- Déchiffrement de la clé symétrique : 


  
- Déchiffrement des données :

``` 
  └─$ openssl enc -d -aes-256-cbc -pbkdf2 -in Plástico_Rubén_Blades.enc -out Plástico_Rubén_Blades_decodé.txt -kfile cle_session.key
                                                                                                                                                             
┌──(dane㉿Dane)-[~]
└─$ cat Plástico_Rubén_Blades_decodé.txt 
[Letra de Plástico]

[Verso 1]
Ella era una chica plástica de esas que veo por ahí
De esas que cuando se agitan, sudan Chanel number three
Que sueñan casarse con un doctor
Pues el puede mantenerlas mejor
No le hablan a nadie si no es su igual
```



         



