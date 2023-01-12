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
    [a, b]  % \(a_n, b_n\)
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
    [a, b, err]  % \(a_n, b_n, \varepsilon_n\)
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
    [a, b, err]  % \(a_n, b_n, \varepsilon_n\)
end
```

* Module (e)
```matlab
log2((2-0) / 10^-6)
```
