### QAP Representation
```
F13 = GF(13)
F13t.<t> = F13[]
T = F13t((t-5)*(t-7))
A2 = F13t.lagrange_polynomial([(5,1), (7,0)])
A5 = F13t.lagrange_polynomial([(5,0), (7,1)])
T == F13t(t^2 + t + 9)
```
True
```
A2 == F13t(6*t + 10)
```
True
```
A5 == F13t(7*t + 4)
```
True

### QAP Satisfiability
```
F13 = GF(13)
F13t.<t> = F13[]
T = F13t(t^2 + t + 9)
P = F13t((2*(6*t+10)+6*(7*t+4))*(3*(6*t+10)+4*(7*t + 4)) - (11*(7*t+4)+6*(6*t+ 10)))
P == T
```
True
```
P % T 
```
0
```
F13 = GF(13)
F13t.<t> = F13[]
T = F13t(t^2 + t + 9)
P = F13t((2*(6*t+10)+8*(7*t+4))*(3*(6*t+10)+4*(7*t+4))-(8*(6*t+10)+11*(7*t+4)))
P == F13t(8*t^2 + 6)
```
True
```
P % T
```
5*t + 12