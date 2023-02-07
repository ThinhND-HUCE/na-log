```matlab
X = [-1, 0, 1, 2]
Y = [4, 3, 2, 7]
syms x
```
## 1. Phương pháp Lagrange
```matlab
P = 0
for i = 1:4
    L = 1;
    for j = 1:4
        if j ~= i
            L = L * (x - X(j)) / (X(i) - X(j));
        end
    end
    L, expand(L)
    P = P + Y(i) * L;
end
expand(P)
```

## 2. Phương pháp Newton
```matlab
d = zeros(4, 4);
d(1, :) = Y
for k = 2:4
    for i = 1:5-k
        d(k, i) = d(k-1, i+1) - d(k-1, i);
    end
end
d

syms t
```

* Newton tiến
```matlab
P = Y(1);
for k = 1:3
    N = d(k+1, 1) / factorial(k);
    for i = 0:k-1
        N = N * (t - i);
    end
    P = P + N;
end
P = subs(P, t, (x-X(1)) / 1)
expand(P)
```

* Newton lùi
```matlab
P = Y(4);
for k = 1:3
    N = d(k+1, 4-k) / factorial(k);
    for i = 0:k-1
        N = N * (t + i);
    end
    P = P + N;
end
P = subs(P, t, (x-X(4)) / 1)
expand(P)
```
