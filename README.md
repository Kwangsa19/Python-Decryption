# Python-Decryption
> This is inspired by [Imdad Ahad](https://imdad.codes). Please visit this Coursera [link](https://www.coursera.org/projects/decryption-with-python) to get started.
> Encryption converts plaintext into ciphertext while decryption is the inverse process of encryption. 

## 1. Decryption - Remove (;)

Instructions: 
* Simple cipher with Python
* The ciphertext should have ";". For example: H;e;l;l;o; or J;k;r;o;w;l;i;n;g.
* The code will remove ";". Using those two as examples, they would be "Hello" and "Jkrowling".

* Screenshot:
  
![chrome_YX3kvrlUH7](https://github.com/Kwangsa19/Python-Encryption-Decryption/assets/135963482/765680d1-0ed4-43af-abb0-212178609044)


* The code can be found on Jupyter notebook titled "Decrypt - Remove (;)" in `Decrypt` folder. 

## 2. Reverse 
* Decrypt the reverse cipher with Python.
* Reverse the alphabets using this:
```
def reverse_text(message):
	reversed = ''
	i = len(message) - 1
	while i >= 0:
		reversed += message[i]
		i -= 1
	return reversed
```

* Screenshot:
  
![chrome_bw7VlFywwm](https://github.com/Kwangsa19/Python-Encryption-Decryption/assets/135963482/03dbb56c-a862-4e79-a6f4-a3f60b2c35c2)

* The code can be found on Jupyter notebook titled "Decrypt - Reverse" in `Decrypt` folder. 

## 3. Decryption - Caesar
* Decrypt the Caesar cipher with Python
* Decrypt the Caesar cipher text by using this:
```
# Decrypt the ciphertext
def decrypt_text(Ciphertext, key):
	decrypted_plaintext = ''

    # Ciphertext uppercase, lowercase, and others
	for c in Ciphertext:
		if c.isupper():
			alphabet = string.ascii_uppercase
		elif c.islower():
			alphabet = string.ascii_lowercase
		else:
			decrypted_plaintext += c
			continue
		# check position and shift them into 26 alphabet letters
		position = alphabet.find(c)
		shifted_position = (position - int(key)) % 26
		plaintext_letter = alphabet[shifted_position]
		decrypted_plaintext += plaintext_letter
	return decrypted_plaintext
```

* Assuming the key is 4, then the following will be ciphertext and its plaintext:
```
'ABC' -> 'WXY' 
'EFG' -> 'ABC'
And so on...
```

* Screenshot: 

![chrome_z3XQsQusq8](https://github.com/Kwangsa19/Python-Encryption-Decryption/assets/135963482/b2b05cdb-f7d9-44ad-bc64-48c3b5138a29)

* The code can be found on the Jupyter notebook titled "Decryption - Caesar" in `Decrypt` folder. 

## 4. Fernet - Symmetric
* On the hard drive, decrypt the files with Fernet (symmetric encryption)
* Install `cryptography` and import `Fernet` if you have not. 
* Use the following code:
```
def decrypt_file(file_location, key):
	f = Fernet(key)
	with open(file_location, "rb") as file:
		encrypted_data = file.read()
	decrypted_data = f.decrypt(encrypted_data)

	with open("./decrypted.txt", "wb") as file:
		file.write(decrypted_data)
```
* `f = Fernet(key) should be a URL-safe base64-encoded 32-byte key. Fernet uses symmetric encryption which uses the same key for both encryption and decryption.
* Then we open the file in binary mode `with open(file_location, "rb") a file:`. The `with` statement guarantees that the file is closed after we read it. 
*  `with open("./decrypted.txt", "wb")` is to ensure we can write the decrypted data to a new file.

*  Screenshot:
The decrypted file is generated. 

![chrome_RlaTmW6wVt](https://github.com/Kwangsa19/Python-Encryption-Decryption/assets/135963482/ee8c4448-d05a-4c5e-bcd9-6e1ac5cbbadd)

![chrome_TG0lIN3b1Q](https://github.com/Kwangsa19/Python-Encryption-Decryption/assets/135963482/f72ee00d-66e1-4baa-9e18-086237c963f9)

* The code can be found on the Jupyter notebook titled Fernet - Symmetric 

## 5. RSA - Asymmeteric 
* On the hard drive, decrypt files with RSA (asymmetric encryption).
* Install `RSA` and import `RSA`.
* In this scenario, we just need to focus on the private key as we decrypt the encrypted file. 
* Use the following code:
```
def load_private_key(private_key_location):
	private_key = None
	with open(private_key_location, "rb") as file:
		private_key = rsa.PrivateKey.load_pkcs1(
			file.read(), format='PEM'
		)
	return private_key

def rsa_decrypt(encrypted_data, private_key):
	decrypted = rsa.decrypt(
		encrypted_data, private_key).decode('utf-8')
	return decrypted

def run():
	private_key_location = input("Enter the private key location: ")
	private_key = load_private_key(private_key_location)
	encrypted_file_location = input("Enter the location of the encrypted file: ")
	with open(encrypted_file_location, "rb") as file:
		encrypted_data = file.read()
		decrypted_data = rsa_decrypt(
			encrypted_data, private_key
		)
	print(f"The decrypted message is: {decrypted_data}")
```
* Load the private RSA key from a specified file location. It works well with PKCS#1 PEM format.
* The code will open the file in binary read mode and uses `rsa.PrivateKey.load_pkcs1`.
* The public RSA key will encrypt the file while the private RSA will decrypt the file. In this scenario, we assumed the data to be UTF-8 encoded (from bytes to a string).
* The decrypted message is : `I loved this project :)`. 
* Screenshot:
  
![chrome_0WHTtW3ATS](https://github.com/Kwangsa19/Python-Encryption-Decryption/assets/135963482/7630de6a-bb42-47c5-b45c-54e7d195ce21)

![chrome_KwDtbfbTTk](https://github.com/Kwangsa19/Python-Encryption-Decryption/assets/135963482/90da347a-5e91-4b14-92fa-9aaf527dab4a)

* The code can be found on the Jupyter notebook titled RSA - Asymmetric

## Conclusion 
This mini project shows how to decrypt simple encrypted files, including symmetric and asymmetric. 
