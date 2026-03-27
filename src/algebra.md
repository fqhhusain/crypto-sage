## Hash Functions
```
import hashlib
test = 'e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855'
empty_string = ''
binary_string = empty_string.encode()
hasher = hashlib.sha256(binary_string)
result = hasher.hexdigest()
type(result)
```
<class 'str'>
```
d = ZZ('0x' + result)
d.str(16) == test
```
True
```
d.str(16)
```
'e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855'
```
d.str(2)
```
'1110001110110000110001000100001010011000111111000001110000010100100110101111101111110100110010001001100101101111101110010010010000100111101011100100000111100100011001001001101110010011010011001010010010010101100110010001101101111000010100101011100001010101'
```
d.str(10)
```
'102987336249554097029535212322581322789799900648198034993379397001115665086549'
## Pedersen Hashes
```
import hashlib
def SHA256_H(x):
    Z5 = Integers(5)
    hasher = hashlib.sha256(x)
    digest = hasher.hexdigest()
    z = ZZ(digest, 16)
    z_bin = z.digits(base=2, padto= 256)

    return Z5(2)^z_bin[0] * Z5(3)^z_bin[1]

SHA256_H(b"")
```
2
```
SHA256_H(b"SHA")
```
3
```
SHA256_H(b"math")
```
1
# Commutative Rings
```
ZZ
```
Integer Ring
```
ZZ['x']
```
Univariate Polynomial Ring in x over Integer Ring
```
Integers(6)
```
Ring of integers modulo 6
## Hashing into Modular Arithmetic
```
import hashlib
def Hash5(x):
    hasher = hashlib.sha256(x)
    digest = hasher.hexdigest()
    d = ZZ(digest, base=16)
    d = d.str(2)[-4:]
    d = ZZ(d, base=2)
    return d
Hash5(b'')
```
5
```
import hashlib
z23 = Integers(23)
def Hash_mod23(x, k2):
    hasher = hashlib.sha256(x.encode('utf-8))
    digest = hasher.hexdigest()
    d = ZZ(digest, base=16)
    d = d.str(2)[-k2:]
    d = ZZ(d, base=2)
    return z23(d)
```
# Fields
```
QQ
```
Rational Field
```
F2 = GF(2)
F2(1)
```
1
```
F2(1) + F2(1)
```
0
```
F2(1) / F2(1)
```
1
## Prime Field Extensions
```
Z3 = GF(3)
Z3t.<t> = Z3[]
P = Z3t(t^2+1)
P.is_irreducible()
```
True
```
F3_2.<t> = GF(3^2, name='t', modulus=P)
F3_2
```
Finite Field in t of size 3^2
```
F3_2(t+2)* F3_2(2*t+2) == F3_2(2)
```
True
```
F3_2(2*t+2)^(-1)
```
2*t + 1
```
F3_2(t+1) * (F3_2(t) ** 2 + F3_2(2*t + 2)) == F3_2(2)
```
True
```
F3_2(t+1) * (F3_2(2*t) ** 2 + F3_2(2*t+2)) == F3_2(2)
```
True