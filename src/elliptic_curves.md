## Affine Short Weierstrass Form
```
F5 = GF(5)
a = F5(2)
b = F5(4)
F5(6) * (F5(4) * a^3 + F5(27) * b^2) != F5(0)
```
True
```
E = EllipticCurve(F5, [a, b])
p = E(0,2)
p.xy()
```
(0, 2)
```
INF = E(0)
try:
    INF.xy()
except ZeroDivisionError:
    pass
P = E.plot()
```

```
p = 115792089237316195423570985008687907853269984665640564039457584007908834671663
p.str(16)
```
'fffffffffffffffffffffffffffffffffffffffffffffffffffffffefffffc2f'
```
p.is_prime()
```
True
```
p.nbits()
```
256
```
Fp = GF(p)
secp256k1 = EllipticCurve(Fp, [0,7])
r = secp256k1.order()
r.str(16)
```
'fffffffffffffffffffffffffffffffebaaedce6af48a03bbfd25e8cd0364141'
```
r.is_prime()
```
True
```
r.nbits()
```
256
```
p = 21888242871839275222246405745257275088696311157297823662689037894645226208583
p.is_prime()
```
True
```
p.nbits()
```
254
```
Fbn128base = GF(p)
bn128 = EllipticCurve(Fbn128base,[0,3])
r = bn128.order()
r.is_prime()
```
True
```
r.nbits()
``` 
254
## Affine Group Law
```
F5 = GF(5)
E1 = EllipticCurve(F5, [1,1])
INF = E1(0)
P1 = E1(0,1)
P2 = E1(4,2)
P3 = E1(0,4)
R1 = E1(2,1)
R2 = E1(3,4)
R1 == P1 + P2
```
True
```
INF == P1 + P3
```
True
```
R2 == P2 + P2
```
True
```
R2 == 2*P2
```
True
```
P3 == P3 + INF
```
True
```
F13 = GF(13)
TJJ = EllipticCurve(F13, [8,8])
P = TJJ(4,0)
INF = TJJ(0)
INF == P+P
```
True
``` 
INF == 2*P
``` 
True
```
P = secp256k1.random_point()
Q = secp256k1.random_point()
R = P + Q
P.xy()
```
(40860261597348664589462555485900796835110964527384076818746863840987946233652,
 32070307645077825174811508888944986814963877295397181925586042846908654867218)

## Logarithmic Ordering
```
F13 = GF(13)
TJJ = EllipticCurve(F13, [8,8])
P = TJJ(5,11)
INF = TJJ(0)
10*P == INF
```
True
```
Q = TJJ(9,4)
R = TJJ(4,0)
10*Q == R
```
True
# Montgomery Curves
```
F13 = GF(13)
L_MTJJ = []
for x in F13:
    for y in F13:
        if F13(7) * y^2 == x^3 + F13(6)*x^2 + x:
            L_MTJJ.append((x,y))
MTJJ = Set(L_MTJJ)
```
## Affine Montgomery Coordinate Transformation
```
L_I_MTJJ = []
for (x, y) in L_MTJJ:
    v = (F13(3)*x + F13(6))/(F13(3) *F13(7))
    w = y/F13(7)
    L_I_MTJJ.append((v,w))
I_MTJJ = Set(L_I_MTJJ)
C_WTJJ = EllipticCurve(F13, [8,8])
L_WTJJ = [P.xy() for P in C_WTJJ.points() if P.order() > 1]
WTJJ = Set(L_WTJJ)
WTJJ == I_MTJJ
```
True
```
L_IINV_WTJJ = []
for (v,w) in L_WTJJ:
    x = F13(7) * (v-F13(4))
    y = F13(7) * w
    L_IINV_WTJJ.append((x,y))
IINV_WTJJ = Set(L_IINV_WTJJ)
MTJJ == IINV_WTJJ
```
True

# Twisted Edwards Curves
```
F13 = GF(13)
L_ETJJ = []
for x in F13:
    for y in F13:
        if F13(3)*x^2 + y^2 == 1+ F13(8)*x^2*y^2:
            L_ETJJ.append((x,y))
ETJJ = Set(L_ETJJ)
```
## Embedding Degrees
```
p = ZZ(13)
r = ZZ(5)
k = ZZ(1)
while k < r:
    if (p^k - 1) % r == 0:
        break
    k = k+1
k
```
4
```
r = ZZ(2)
k = ZZ(1)
while k < r:
    if(p^k -1)%r == 0:
        break
    k = k+1
k
```
1
```
p = ZZ(115792089237316195423570985008687907853269984665640564039457584007908834671663)
r = ZZ(115792089237316195423570985008687907852837564279074904382605163141518161494337)
k = ZZ(1)
while k < 1000:
    if (p^k - 1) % r == 0:
        break
    k = k + 1
k
```
1000
```
p = ZZ(21888242871839275222246405745257275088696311157297823662689037894645226208583)
r = ZZ(21888242871839275222246405745257275088548364400416034343698204186575808495617)
k = ZZ(1)
while k < 50:
    if(p^k-1)%r == 0:
        break
    k = k + 1
k
```
12

### Elliptic Curves over Extension Fields
```
F5 = GF(5)
F5t.<t> = F5[]
P_MOD_2 = F5t(t^2+2)
P_MOD_2.is_irreducible()
```
True
```
F5_2.<t> = GF(5^2, name='t', modulus= P_MOD_2)
E1F5_2 = EllipticCurve(F5_2, [1,1])
E1F5_2.order()
```
27
## Full Torsion Groups
```
INF = E1F5_2(0)
L_E1_3 = []
for p in E1F5_2:
    if 3*p == INF:
        L_E1_3.append(p)
E1_3 = Set(L_E1_3)
E1_3
```
{(1 : t : 1), (2 : 1 : 1), (0 : 1 : 0), (2 : 4 : 1), (2*t + 1 : t + 1 : 1), (2*t + 1 : 4*t + 4 : 1), (3*t + 1 : t + 4 : 1), (1 : 4*t : 1), (3*t + 1 : 4*t + 1 : 1)}
```
F13 = GF(13)
F13t.<t> = F13[]
P_MOD_4 = F13t(t^4+2)
P_MOD_4.is_irreducible()
```
True
```
F13_4.<t> = GF(13^4, name='t', modulus=P_MOD_4)
TJJF13_4 = EllipticCurve(F13_4, [8,8])
INF = TJJF13_4(0)
L_TJJF13_4_5 = INF.division_points(5)
TJJF13_4_5 = Set(L_TJJF13_4_5)
TJJF13_4_5.cardinality()
```
25
```
P_MOD_3 = F13t(t^3 + 2)
P_MOD_3.is_irreducible()
```
True
```
F13_3.<t> = GF(13^3, name='t', modulus=P_MOD_3)
TJJF13_3 = EllipticCurve(F13_3, [8,8])
INF = TJJF13_3(0)
L_TJJF13_3_5 = INF.division_points(5)
TJJF13_3_5 = Set(L_TJJF13_3_5)
TJJF13_3_5.cardinality()
```
5
## Pairing Groups
```
L_G1 = []
for P in E1_3:
    PiP = E1F5_2([a.frobenius() for a in P])
    if P == PiP:
        L_G1.append(P)
G1 = Set(L_G1)
G1
```
{(2 : 1 : 1), (2 : 4 : 1), (0 : 1 : 0)}
```
L_G2 = []
for P in E1_3:
    PiP = E1F5_2([a.frobenius() for a in P])
    pP  = 5*P
    if pP == PiP:
        L_G2.append(P)
G2 = Set(L_G2)
```
```
L_TJJ_G1 = []
for P in TJJF13_4_5:
    PiP = TJJF13_4([a.frobenius() for a in P])
    if P == PiP:
        L_TJJ_G1.append(P)
TJJ_G1 = Set(L_TJJ_G1)
TJJ_G1
```
{(7 : 11 : 1), (0 : 1 : 0), (8 : 8 : 1), (7 : 2 : 1), (8 : 5 : 1)}
```
L_TJJ_G2 = []
for P in TJJF13_4_5:
    PiP = TJJF13_4([a.frobenius() for a in P])
    pP = 13*P
    if pP == PiP:
        L_TJJ_G2.append(P)
TJJ_G2 = Set(L_TJJ_G2)
TJJ_G2
```
## The Weil Pairing
```
F13 = GF(13)
F13t.<t> = F13[]
P_MOD_4 = F13t(t^4+2)
F13_4.<t> = GF(13^4, name='t', modulus=P_MOD_4)
TJJF13_4 = EllipticCurve(F13_4, [8,8])
P = TJJF13_4(7,2)
Q = TJJF13_4([9*t^2+7, 12*t^3+2*t])
P.weil_pairing(Q, 5)
```
7*t^3 + 7*t^2 + 6*t + 3
## Try-and-increment Hash Functions
```
import hashlib
def try_hash(s,c):
    s_1 = s+c
    hasher = hashlib.sha256(s_1.encode('utf-8'))
    digest = hasher.hexdigest()
    z = ZZ(digest, 16)
    z_bin = z.digits(base=2, padto=256)
    x = z_bin[0]*2^0 +z_bin[1]*2^1 + z_bin[2]*2^2 + z_bin[3]*2^3
    return (x, z_bin[4])
try_hash('1110010000','1') 
```
(3, 1)
```
try_hash('1110010000','10')
```
(12, 1)
```
TJJ = EllipticCurve(F13, [8,8])
P = TJJ(12,8)
(4*P).xy()
```
(8, 8)
## The Trace of Frobenius
```
p = 115792089237316195423570985008687907853269984665640564039457584007908834671663
r = 115792089237316195423570985008687907852837564279074904382605163141518161494337
t = p + 1 - r
t.nbits()
```
129
```
abs(RR(t)) <= 2*sqrt(RR(p))
```
True
```
p = 115792089237316195423570985008687907853269984665640564039457584007908834671663
F = GF(p)
j = F(1728) * ((F(4) * F(0)^3)/(F(4)*F(0)^3+F(27)*F(7)^2))
j == F(0)
```
True
## The Complex Multiplication Method
```
z = ComplexField(100) (0,1)
z
```
1.0000000000000000000000000000*I
```
elliptic_j(z)
```
1728.0000000000000000000000000
```
z = ComplexField(100)(1, -1)
try:
    elliptic_j(z)
except PariError:
    pass
z = ComplexField(100)(-1, sqrt(3))/2
elliptic_j(z)
```
-2.6445453750358706361219364880e-88
```
elliptic_j(z).imag().round()
```
0
```
elliptic_j(z).real().round()
```
0
```
D = -3
p = 115792089237316195423570985008687907853269984665640564039457584007908834671663
r = 115792089237316195423570985008687907852837564279074904382605163141518161494337
t = p + 1 - r
v_sqr= (4*p - t^2)/abs(D)
v_sqr.is_integer()
```
True
```
v = sqrt(v_sqr)
v.is_integer()
```
True
```
4*p == t^2 + abs(D) * v^2
```
True
```
303414439467246543595250775667605759171
```
F = GF(p)
for c2 in F:
    try:
        _ = c2.nth_root(2)
    except ValueError:
        break
c2
```
3
```
for c3 in F:
    try:
        _ = c3.nth_root(3)
    except ValueError:
        break
c3
```
2
```
C1 = EllipticCurve(F,[0,1])
C1.order() == r
```
False
```
C2 = EllipticCurve(F, [0, c2^3])
C2.order() == r
```
False
```
C3 = EllipticCurve(F, [0, c3^2])
C3.order() == r
```
False
```
C4 = EllipticCurve(F, [0, c3^2*c2^3])
C4.order() == r
```
False
```
C5 = EllipticCurve(F, [0, c3^(-2)])
C5.order() == r
```
False
```
C6 = EllipticCurve(F, [0, c3^(-2)*c2^3])
C6.order() == r
```
True
```
b1=F(86844066927987146567678238756515930889952488499230423029593188005931626003754)
for b2 in F:
    if b2 == 0: continue
    try:
        d = (b2/b1).nth_root(3)
        _ = d.nth_root(2)
    except ValueError: continue
    break
b2
```
7
```
## The BLS6_6 Pen-and-paper Curve
### The Construction
```
k = 0
for k in range(1, 42):
    if (43^k-1)%13 == 0:
        break
k
```
6
```
F43 = GF(43)
c2 = F43(5)
try:
    c2.nth_root(2)
except ValueError:
    print("OK")
c3 = F43(36)
try: 
    c3.nth_root(3)
except ValueError:
    print("OK")
```
OK
OK
```
BLS61 = EllipticCurve(F43, [0,1])
BLS61.order() == 39
```
False
```
BLS62 = EllipticCurve(F43, [0, c2^3])
BLS62.order() == 39
```
False
```
BLS63 = EllipticCurve(F43, [0, c3^2])
BLS63.order() == 39
```
True
```
BLS64 = EllipticCurve(F43, [0, c3^2*c2^3])
BLS64.order() == 39
```
False
```
BLS65 = EllipticCurve(F43, [0, c3^(-2)])
BLS65.order() == 39
```
False
```
BLS6 = BLS63
```
### The Large Prime Order Subgroup
``` 
P1 = BLS6(9,2)
g1 = 3*P1
g1.xy()
```
(13, 15)
```
G1_13 = [x*g1 for x in range(0,13)]
G1_13
```
[(0 : 1 : 0),
 (13 : 15 : 1),
 (33 : 34 : 1),
 (38 : 15 : 1),
 (35 : 28 : 1),
 (26 : 34 : 1),
 (27 : 34 : 1),
 (27 : 9 : 1),
 (26 : 9 : 1),
 (35 : 15 : 1),
 (38 : 28 : 1),
 (33 : 9 : 1),
 (13 : 28 : 1)]
```
### Pairing Groups
```
F43 = GF(43)
F43t.<t> = F43[]
p = F43t(t^6+6)
p.is_irreducible()
```
True
```
F43_6.<v> = GF(43^6, name='v', modulus=p)
F43_6.order()
```
6321363049
``` 
ExtBLS6 = EllipticCurve(F43_6, [0, 6])
INF = ExtBLS6(0)
for P in INF.division_points(13):
    if P.order() == 13:
        piP = ExtBLS6([a.frobenius() for a in P])
        qP = 43*P
        if piP == qP:
            break
P.xy()
```
(7*v^2, 16*v^3)
``` 
g2 = ExtBLS6(7*v^2, 16*v^3)
G2_13 = [x*g2 for x in range(0,13)]
G2_13
```
[(0 : 1 : 0),
 (7*v^2 : 16*v^3 : 1),
 (10*v^2 : 28*v^3 : 1),
 (42*v^2 : 16*v^3 : 1),
 (37*v^2 : 27*v^3 : 1),
 (16*v^2 : 28*v^3 : 1),
 (17*v^2 : 28*v^3 : 1),
 (17*v^2 : 15*v^3 : 1),
 (16*v^2 : 15*v^3 : 1),
 (37*v^2 : 16*v^3 : 1),
 (42*v^2 : 27*v^3 : 1),
 (10*v^2 : 15*v^3 : 1),
 (7*v^2 : 27*v^3 : 1)]
```
### The Weil Pairing
```
g1 = ExtBLS6([13,15])
g2 = ExtBLS6([7*v^2, 16*v^3])
g1.weil_pairing(g2, 13)
```
5*v^5 + 16*v^4 + 16*v^3 + 15*v^2 + 3*v + 41
