## 1. Phương pháp chia đôi
* Module (a)
```matlab
f = @(x) x^3 + 2*x - 1
f(0)                    % -1
f(2)                    % 11
```

* Module (b)
```matlab
a = 0;
b = 2;
for n = 1:5
    c = (a+b) / 2;
    if f(c) == 0
        c
        break
    elseif f(a) * f(c) < 0
        b = c;
    else
        a = c;
    end
    [a, b]
end
```

* Module (b, c)
```matlab
a = 0;
b = 2;
for n = 1:5
    c = (a+b) / 2;
    if f(c) == 0
        c
        break
    elseif f(a) * f(c) < 0
        b = c;
    else
        a = c;
    end
    err = b - a
    [a, b, err]
end
```

* Module (d)
```matlab
a = 0;
b = 2;
while b - a > 10^-2
    c = (a+b) / 2;
    if f(c) == 0
        c
        break
    elseif f(a) * f(c) < 0
        b = c;
    else
        a = c;
    end
    err = b - a
    [a, b, err]
end
```

* Module (e)
```matlab
log2((2-0) / 10^-6)
```


## 2. Phương pháp Newton
* Module (a)
```matlab
f = @(x) x^3 - x^2 - 3

% Cách 1
syms x
fplot(f(x), [1, 4])

% Cách 2
diff(f(x), 2)
subs(diff(f(x)), 1)
f(1), f(4)
```

* Module (b)
```matlab
syms t
df = @(x) subs(diff(f(t)), x)
df(x)

x = zeros(1, 4)
x(1) = 4
for n = 1:3
    x(n+1) = x(n) - f(x(n)) / df(x(n))
end
```

* Module (c)
```matlab
M = 22
m = min(abs(df(1)), abs(df(4)))

e = zeros(1, 4)
for n = 2:4
    e(n) = M / 2 / m * (x(n) - x(n-1))^2
end
```

* Module (d)
```matlab
x0 = 4
while true
    x = vpa(x0 - f(x0) / df(x0))
    e = vpa(M / 2 / m * (x - x0)^2)
    x0 = x;
    if e < 10^-6
        break
    end
end
```

* Module (e)
```matlab
x = zeros(1, 4)
x(1) = 4
for n = 1:3
    x(n+1) = x(n) - f(x(n)) / df(4)
end
```

* Module (f): thực hành tìm $M$
```matlab
% Cách 1
X = linspace(1, 4, 101)
d2f = @(x) -abs(subs(diff(f(t), 2), x))
Y = abs(vpa(d2f(X)))
M = max(Y)

% Cách 2
g = @(x) -abs(subs(diff(f(t), 2), x))
[xmin, M] = fminbnd(g, 1, 4)
vpa(-M)
```


## 3. Phương pháp lặp điểm bất động
* Module (a)
```matlab
g = @(x) nthroot(x^2 + 3, 3)

% Cách 1
syms x
diff(g(x))

g(1), g(4)

simplify( diff(g(x), 2) )

syms t
dg = @(x) subs(diff(g(t)), t, x)

for x = [1, 4, 3]
    vpa(abs(dg(x)))
end

q = vpa(abs(dg(3)))


% Cách 2
syms x
fplot(g(x), [1, 4])
fplot(abs(dg(x)), [1, 4])

X = linspace(1, 4, 101)
Y = abs(vpa(dg(X)))
q = max(Y)
```

* Module (b)
```matlab
x = zeros(1, 4);
x(1) = 2.5;
for n = 1:3
    x(n+1) = g(x(n));
end

x
```

* Module (c)
```matlab
e = zeros(1, 4);
for n = 2:4
    e(n) = q / (1-q) * abs(x(n) - x(n-1));
end

e
```

* Module (d)
```matlab
x0 = 2.5;
while true
    x = g(x0)
    e = q / (1-q) * abs(x - x0)
    x0 = x;
    if e < 10^-4
        break
    end
end
```

* Module (e)
```matlab
x0 = 2.5
x1 = g(x0)
log(10^-10 * (1-q) / abs(x1 - x0)) / log(q)
```



