# TP1 CyberChef

## I. Partie 1 : Chiffrement de César

### 1. 
  ![alt text](Images/I_1.png)
### 2. 
  ![alt text](Images/image.png)

## II. Partie 2 : Vigenère

### 1.
 ![alt text](Images/image-2.png)
### 2.
 ![alt text](Images/image-1.png)

## III. Partie 3 : Chiffrement symétrique AES

### Découverte

#### 1. Chiffrement de la chaîne TESTSECRET1234567 

![alt text](Images/image-3.png)

#### 2. On constate que si on modifie 1 caractère du texte initial toute le résultat change.

#### 3. Déchiffrement du texte AES 

![alt text](Images/image-4.png)

### Transmission du message chiffré

#### 1. Generation des clés  

![alt text](Images/image-5.png)

#### 2 Chiffrement du message 

![alt text](Images/image-6.png)


- **cle :**  d529dc588dc7ab4c72dc98b03ccaa9cdff081b99ed9107e51761ddb30a3f500d

- **message :** 71ffa545ca5209ea7d78513630b83b5153a02b53a42ead45c366879b0756c4ce

#### 6 Message chiffré du binôme  

![alt text](Images/image-7.png)

## IV. Partie 4 : RSA

### Génération d’une paire de clés RSA

- RSA Key Pair Généré avec "Generate RSA Key Pair" d'une taille de 1024 bits

  ![alt text](Images/image-8.png)

  ```
  -----BEGIN PUBLIC KEY-----
  MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDRdo4PYiKOkuRYd1NsiHlKjzq2
  wVMYlj5hqWSXnWC8p2D2vNT92oxv42A8NBEPfYZiv2VAeqHK7Wj7HHgg4MXu8nyk
  jGc4cXgILjSudgD41Q1wEkurtADz2xml7A3iDXO+dT1BmEPWsIgjpIfPN7oqEcVI
  ePTZz5mJWagWO691qQIDAQAB
  -----END PUBLIC KEY-----

  -----BEGIN RSA PRIVATE KEY-----
  MIICWwIBAAKBgQDRdo4PYiKOkuRYd1NsiHlKjzq2wVMYlj5hqWSXnWC8p2D2vNT9
  2oxv42A8NBEPfYZiv2VAeqHK7Wj7HHgg4MXu8nykjGc4cXgILjSudgD41Q1wEkur
  tADz2xml7A3iDXO+dT1BmEPWsIgjpIfPN7oqEcVIePTZz5mJWagWO691qQIDAQAB
  AoGAEMm/FRM5JdLheQhcqARALxj6YboY842HLm3/NqT8eI0Jw9IwArCeNObfyF4m
  nTvi+3h6SwgJKP83kiN0AAlD6SphON9z9ivqZ+z/r+4fC75g+cgUhphA7LgL18IT
  4NmQP4nzP2Z2p1+IhaoS804TOr9HsyqNzyEc0vLJd501nIkCQQDxFyy+c4SDlSFF
  vMTltMaHPpv4LGlEwSsIyAew2FOThdPwDLBZkT6H7RhWbb72gRn6/Ujh8CUbQTtp
  ofCG/rCPAkEA3mqrqRDmASh5T511rRHp1/V8So1GbO7l++m4U2aKeXxm/DuEIehX
  2VTm2mcAQGJzCHaV6lgHg0CuIZXvUI6iRwJAIicqS4CJ0SobIInxSqklRptz9OA1
  uWuz8PaFQGQk0s0ujN7/THDq7s6DmBrL5pe7WnbvEDK4zveatwgdzsHduQJAeNI3
  d/rvBvgGlkIyF5cgkakQIKuH80r/cg4vjFaqqH30r9Zg286MUko1sbS8RT11wcYx
  gADb6+fp7+K0Au3IpwJAJRKjZGznY7iX9KpIAJfVzahzrxwxwrOVlzXGbKz+aSEc
  gRQ1P9ppK2F48UDYHMMVn2zsQGGFcu4tFAQQUtxszA==
  -----END RSA PRIVATE KEY-----
  ```

- **Les clés générées contiennent :**

  - Une Clé Publique de 222 caractères.
  - Une Clé Privé de 836 caractères.
  - Avec une titre de commencement et de fin :  
    - BEGIN PUBLIC KEY/END PUBLIC KEY
    - BEGIN RSA PRIVATE KEY/END RSA PRIVATE KEY

### 2. Découverte

- Chiffrement du message LE MESSAGE EST SECRETSIMPLE avec la "PUBLIC KEY"

  ![alt text](Images/image-9.png)

    - La sortie chiffrée contiens des "Raw bytes" : 
      ```
      ]¹¦²okù¥a¹¾¯Þ/u³rW®}½0'n_§æ3f9ÖYâ'¢¸.«f@ã ²6ÍÀIWÛ_f¤êQù¿ô×è BµcyL¯íák ±_ |d¨ áâ9I½02VL.C¶hd¿°GåïØ
      ```

      Pour le transformer j'ajoute la fonctionnalité "To base64" pour transformer la sortie en "ASCII Base64 string".

- Processus inverse pour le déchiffrer " From Base64"

  ![alt text](Images/image-10.png)
    
    - La sortie est identique au message d'origine.

### 3. Transmission d’un message chiffré à votre binôme
- Clé PUBLIQUE du binôme :
  ```
  -----BEGIN PUBLIC KEY-----
  MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDNc7aNMgbR1CgPaTdwYjM49xpJ
  CUxV0Ny9A84PsEpqbv2Rsylyq+THhs2MiYFif9Y6k+YCMBIfSjeXAhQcySpQLlP0
  jxmC33N7MfTQsXw+At/KPFvsNIGuj4MTiFTQoRde+VzG6oOIwRZtSc3Dy6mtAc4H
  iNMJYkTef64LmiSVewIDAQAB
  -----END PUBLIC KEY-----
  ```
- Chiffrement d'une réplique

  ![alt text](Images/image-16.png)

- Transmission du texte du sortie précédente (en Base64) au binôme et déchiffrement avec la cé PRIVÉE du texte (en Base64) reçu du binôme :

  ![alt text](Images/image-17.png)

## V. Partie 5 : Hachage

- Hachage sur la chaîne **"admin123"** :

  - **SHA-1** : f865b53623b121fd34ee5426c792e5c33af8c227
  - **SHA-2** : 
    - **256** : 240be518fabd2724ddb6f04eeb1da5967448d7e831c08c8fa822809f74c720a9
    - **512** : 7fcf4ba391c48784edde599889d6e3f1e47a27db36ecc050cc92f259bfac38afad2c68a1ae804d77075e8fb722503f3eca2b2c1006ee6f6c7b7628cb45fffd1d
  - **SHA-3** : 
    - **256** : b227bff0d28823d4599a39a5b55725b0811c9c13184087e9a122eb572e6ff139
    - **512** : 9150a266c71a4cf0cbd01a60608f395ec1f8f7082f4041e49195cad98f6ee0cb08efe60cb8d148d2e40520b33922bf40
- Tailles des hashs produits :  
  - **SHA-1** : 40 Caractères 
  - **SHA-2** : 
    - **256** : 64 Caractères
    - **512** : 128 Caractères
  - **SHA-3** : 
    - **256** : 64 Caractères
    - **512** : 128 Caractères
  
  - Il est possible de retrouver les mot de passe en passant par des Lookup Tables (tables de correspondance).

  - Le Hash change radicalement sur deux textes légèrement différents :
    - TEST : SHA2 256      94ee059335e587e501cc4bf90613e0814f00a7b08bc7c648fd865a2af6a22cc2
    - TESt : SHA2 256      88ce93c579bc13c149b6dee231497aa38a70d0e9ee6b365f10f10c5007548169

-  « hello » en SHA1 (80 rounds) : "aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d"
   - Cracke sur https://crackstation.net/ : 
    ![alt text](Images/image-12.png) 
      - Les hashes et mdp sont dans de tables appelés "Rainbow tables" crées à partir des base des données des mdp qui ont fuités, donc en parcourant de façon scripté cette liste en comparant les déférents hash, on retrouve celui qui correspond.
-  Avec SHA1 (50 rounds) : 
   -  Hash : 8b7742d17e2ad77b0dac165c17aae481795cca57 
   -  Type : Unknown 
   -  Result : Not found.
   On peut déduire que personne à répertorié dans les bases des donnés le hash de "hello" passé 50 fois, le plus courante c'est 80, donc n'est pas cracké.

## VI. Partie 6 : Encodage
 
- Encodage du mot "Bonjour" To Base64 --> "Qm9uam91cg=="
 - Ce qui signifie : C'est l'encodage du des caractères du mot "Bonjour". Donc la fonction prenne les codes binaires de chaque lettre, il le découpe en blocs de 6 bits (chaque groupe des 6 bits correspond à un chiffre entre 0 et 63) dans le cas du Base 64 et renvoi un caractère dans la table Base64. Les deux signes == vers la fin c'est pour remplir les espaces vides du dernière block.

- Décodage du résultat précédent : Qm9uam91cg== From Base64 -> "Bonjour"
  - Encodage et chiffrement sont deux choses different 
    - L'Encodage (ex: Base64, ASCII) : Son but est la compatibilité. On transforme la donnée pour qu'elle puisse être lue ou transmise correctement par différents systèmes. Ce n'est pas un secret. N'importe qui peut l'inverser instantanément car la "méthode" est publique et universelle.

    - Le Chiffrement (ex: AES, RSA) : Son but est la confidentialité. On transforme la donnée pour qu'elle soit illisible pour toute personne ne possédant pas la clé. Sans la clé, même si vous connaissez l'algorithme, vous ne pouvez pas retrouver le message original.

## VII. Bonus

Clé et Message cachée dans les "Notes" de la diapositive 13 et 12.
Déchiffré avec CyberChef (Avec outils "AES Décrypte" et "Magic")

![alt text](Images/image-13.png)

![alt text](Images/image-14.png)

![alt text](Images/image-15.png)
