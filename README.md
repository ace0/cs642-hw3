# CS 642: Computer Security - Homework Three

This homework assignment covers topics in cryptography. You must work with a partner. There are two parts; both are required.

It is due **April 28, 2016** by 11:59 PM local time. 

## Part A: Password Cracking

A colleague has built a password hashing mechanism. It applies SHA-256 to a string of the form `username,password,salt` where `salt` is a randomly chosen value. For example, the stored value for username `user` and password `12345` and salt `999999` is 
`c50603be4fedef7a260ef9181a605c27d44fe0f37b3a8c7e8dbe63b9515b8e96`.

For example, the Python code to generate this is:
```
import hashlib;
print hashlib.sha256("user,12345,999999").hexdigest();
```

The same process was used to generate the challenge hash 
`83c02558e533b6051e6d40e84bd03d19193b7090fa016b9b247f86d129d5f608` 
for user `ace` and salt `8593018378`.

* Recover the password used to generate the challenge hash above. *Hint:* The password consists only of numbers.
* Give a pseudocode description of your algorithm and the worst case running time for it.
* Discuss the merits of your colleague’s proposal. Suggest how your attack might be made intractable.
* Put your solutions in the file `solutions.txt`.


## Part B: Encryption

Another colleague decided to build a symmetric encryption scheme. These are implemented in `badencrypt.py` and `baddecrypt.py` and are designed to encrypt a sample message to demonstrate the encryption scheme. To use this demonstationg software, run:
```
CT=$(python badencrypt.py testkeyfile)
echo $CT
python baddecrypt.py testkeyfile $CT
```

Your job is to assess the security of this encryption scheme. Your solution will be a Python program `attack.py` that takes as input a ciphertext and modifies the ciphertext so that the decrypted message has a different (and more lucrative) `AMOUNT` field and still passes the verification in `baddecrypt.py`. `attack.py` must do this without access to the keyfile or knowledge of the key. You can assume the ciphertext contains the sample message hardcoded in `badencrypt.py`.

We will test your solution with original versions of `badencrypt.py` and `baddecrypt.py` and with different encryption keys than the test key provided. To ensure that `attack.py` produces the correct formatted output, you can run from the command line:
```
CT=$(python badencrypt.py testkeyfile)
MODCT=$(python attack.py $CT)
python baddecrypt.py testkeyfile $MODCT
```

In `solutions.txt`, describe what is wrong with your colleague's scheme and how it should be fixed so that it will be more secure.

Your attack script will not have direct access to the key file and should not attempt to gain access to the process memory of baddecrypt or any other files to steal the key directly.

