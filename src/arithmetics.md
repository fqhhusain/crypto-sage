## Integers, Natural Numbers and Rational Numbers

```
ZZ
```
Integer Ring
```
NN
```
Non negative integer semiring
```
QQ
```
Rational Field
```
ZZ(5)
```
5
```
ZZ(5) + ZZ(3)
```
8
```
ZZ(5) * ZZ(3)
```
15
```
ZZ.random_element(10**6)
```
860813
### Prime numbers
```
n = NN(504)
factor(n)
```
## Euclidean Division
```
ZZ(-17) // ZZ(4)
```
-5
```
ZZ(-17) % ZZ(4)
```
3
```
ZZ(4).divides(ZZ(-17))
```
False
```
ZZ(4).divides(ZZ(12))
```
True
```
ZZ(-17) // ZZ(-4)
```
4
```
ZZ(-17) % ZZ(-4)
```
-1
```
ZZ(-17).quo_rem(ZZ(-4))
```
(4, -1)
```
ZZ(143785).quo_rem(ZZ(17))
```
(8457, 16)
```
ZZ(143785) == ZZ(8457) * ZZ(17) + ZZ(16)
```
True
```
ZZ(12).xgcd(ZZ(5))
```
(1, -2, 5)
## Integer Representations
```
NN(27713).str(2)
```
'110110001000001'
```
ZZ(27713).str(16)
```
'6c41'
## Computational Rules
```
ZZ(137).gcd(ZZ(64))
```
1
```
ZZ(64)^ZZ(137) % ZZ(137) == ZZ(64) % ZZ(137)
```
True
```
ZZ(64)^ZZ(137-1) % ZZ(137) == ZZ(1) % ZZ(137)
```
True
```
ZZ(1918).gcd(ZZ(137))
```
137
```
ZZ(1918) ^ ZZ(137) % ZZ(137) == ZZ(1918) % ZZ(137)
```
True
```
ZZ(1918) ^ ZZ(137-1) % ZZ(137) == ZZ(1) % ZZ(137)
```
False
```
(ZZ(7) * (ZZ(2)*ZZ(4) + ZZ(21)) + ZZ(11)) % ZZ(6) == (ZZ(4) - ZZ(102)) % ZZ(6)
```
True
```
(ZZ(7)* (ZZ(2)*ZZ(76) + ZZ(21)) + ZZ(11)) % ZZ(6) == (
ZZ(76) - ZZ(102)) % ZZ(6)
```
True
## The Chinese Remainder Theorem
```
CRT_list([4,1,3,0], [7,3,5,11])
```
88
## Remainder Class Representation
```
Z6 = Integers(6)
Z6(2) + Z6(5)
```
1
```
Z6(7)*(Z6(2)*Z6(4)+Z6(21))+Z6(11) == Z6(4) - Z6(102)
```
True
## Modular Inverses
```
ZZ(6).xgcd(ZZ(5))
```
(1, 1, -1)
```
Z5 = Integers(5)
Z5(3)**(5-2)
```
2
```
Z5(3)**(-1)
```
2
```
Z5(3)**(5-2) == Z5(3)**(-1)
```
True

## Polynomial Arithmetic

```
Zx = ZZ['x']
Zt.<t> = ZZ[]
Zx
```
Univariate Polynomial Ring in x over Integer Ring
```
Zt
```
Univariate Polynomial Ring in t over Integer Ring
```
p1 = Zx([17, -4, 2])
p1
```
2*x^2 - 4*x + 17
```
p1.degree()
```
2
```
p1.leading_coefficient()
```
2
```
p2 = Zt(t^23)
p2
```
t^23
```
p6 = Zx([0])
p6.degree()
```
-1
```
Z6 = Integers(6)
Z6x = Z6['x']
Z6x
```
Univariate Polynomial Ring in x over Ring of integers modulo 6
```
p1 = Z6x([5, -4, 2])
p1
```
2*x^2 + 2*x + 5
```
p1 = Z6x([17, -4, 2])
p1
```
2*x^2 + 2*x + 5
```
Z6x(x-2) * Z6x(x+3)*Z6x(x-5) == Z6x(x^3+ 2*x^2 + x)
```
True
```
Zx = ZZ['x']
p1 = Zx([17,-4,2])
p7 = Zx(x-2) * Zx(x+3) * Zx(x-5)
p1(ZZ(2))
```
17
```
p7(ZZ(-6)) == ZZ(-264)
```
True
```
Z6 = Integers(6)
Z6x = Z6['x']
p1 = Z6x([5, -4,2])
p1(Z6(2)) == Z6(5)
```
True
```
Zx = ZZ['x']
P = Zx([2, -4, 5])
Q = Zx([5, 0, -2, 1])
P + Q == Zx(x^3 + 3*x^2 -4*x + 7)
```
True
```
P * Q == Zx(5*x^5 - 14*x^4 + 10*x^3 + 21*x^2 -20*x + 10)
```
True
```
Z6x = Integers(6)['x']
P = Z6x([2, -4, 5])
Q = Z6x([5, 0, -2, 1])
P + Q == Z6x(x^3 + 3*x^2 + 2*x + 1)
```
True
```
P *Q == Z6x(5*x^5 + 4*x^4 + 4*x^3 + 3*x^2 + 4*x + 4)
```
True
## Euclidean Division with Polynomials
```
Zx = ZZ['x']
A = Zx([-9, 0,0,2,0,1])
B = Zx([-1, 4, 1])
Q = Zx([-80, 19, -4, 1])
P = Zx([-89, 339])
A == Q*B + P
```
True
## Prime Factors
```
Zx = ZZ['x']
p = Zx(x^2 - 3)
p.factor()
```
x^2 - 3
```
Zx = ZZ['x']
p = Zx(x^7 + 3*x^6 + 3*x^5 + x^4 - x^3 - 3*x^2 - 3*x - 1)
p.factor()
```
(x - 1) * (x + 1)^4 * (x^2 + 1)
## Lagrange Interpolation
```
Qx = QQ['x']
S = [(0,4), (-2,1), (2,3)]
Qx.lagrange_polynomial(S)
```
-1/2*x^2 + 1/2*x + 4
```
F5 = GF(5)
F5x = F5['x']
S = [(0,4), (-2,1), (2,3)]
F5x.lagrange_polynomial(S)
```
2*x^2 + 3*x + 4
