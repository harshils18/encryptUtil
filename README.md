# encryptUtil

Create a utility that will perform a simple XOR cryptographic transform on a given set of data - an XOR stream encryptor. The encryption key will be provided by the binary data in an arbitrarily-sized external file. The size of the key in bytes will dictate the "block size.” The plaintext data will be given on stdin, where the utility will then break it into block-sized sections, XOR it against the key, and write the cypher text to stdout. After each block is processed, the key should be rotated to the left by one bit to make a new key. This means that the key will repeat every N blocks, where N is the number of bits in the key. The plaintext data need not be a multiple of the block size in length, nor should it be assumed to be ASCII or Unicode text. It is also valid for the plaintext to be extremely large, far exceeding the available memory+swap space for the system.

In addition to correctly performing the transform, the utility should be able to take advantage of multi-core or multi-processor machines by implementing a multi-threading scheme that processes multiple blocks of plaintext in parallel. The number of threads should be specified as a command-line argument and, regardless of how many are used, the output cypher text should remain the same. All error and/or status information should be printed on stderr.

The utility should be written in C or C++ and should build on a UNIX platform. Please make sure that your submission compiles and runs correctly with a variety of different inputs. Finally, keep in mind that you will be evaluated not only on the correctness of your solution, but also the organization and efficiency of your code.

It is highly suggested that you provide data that shows you tested your solution and that it works as defined.


Required command-line options:

encryptUtil [-n #] [-k keyfile]
-n #        Number of
threads to create
-k keyfile    Path to file containing
key

Example input/output:

$ ls -al
total 56
drwxr-xr-x   5 user  staff 
  170 Jun 16 15:40 .
drwxr-xr-x  35 user 
staff   1190 Jun 16 15:39 ..
-rwxr-xr-x   1 user  staff 
18293 Jun 16 15:35 encryptUtil
-rw-r--r--   1 user  staff 
    2 Jun 16 15:37 keyfile
-rw-r--r--   1 user  staff 
    8 Jun 16 15:38 plaintext

$ hexdump -C keyfile 
00000000  f0 f0         
               
               
   |??|

$ hexdump -C plaintext 
00000000  01 02 03 04 11 12 13 14   
               
       |........|

$ cat plaintext | encryptUtil -n 1 -k keyfile >
cyphertext

$ hexdump -C ciphertext 
00000000  f1 f2 e2 e5 d2 d1 94 93   
               
       |??????..|
