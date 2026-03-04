```
sage: ZZ
Integer Ring
sage: NN
Non negative integer semiring
sage: QQ
Rational Field
sage: ZZ(5)
5
sage: ZZ(5) + ZZ(3)
8
sage: ZZ(5) * NN(3)
15
sage: ZZ.random_element(10**6)
938288
sage: n = NN(504)
sage: factor(n)
2^3 * 3^2 * 7
sage: ZZ(-17) // ZZ(4)
-5
sage: ZZ(4).divides(ZZ(-17))
False
sage: ZZ(4).divides(ZZ(12))
True
sage: ZZ(-17) // ZZ(-4)
4
sage: ZZ(-17) % ZZ(-4)
-1
sage: ZZ(-17).quo_rem(ZZ(-4))
(4, -1)
sage: ZZ(143785).quo_rem(ZZ(17))
(8457, 16)
sage: ZZ(143785) == ZZ(8457)*ZZ(17) + ZZ(16)
True
```