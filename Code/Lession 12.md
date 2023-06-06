# Phương trình elliptic
```matlab
% Bước 1: khai báo f
f = @(x, y) 4

% Bước 2: lưới
a = 0; b = 1; c = 0; d = 2;
n = 4; m = 8;
h = (b-a)/n
k = (d-c)/m
X = linspace(a, b, n+1)
Y = linspace(c, d, m+1)

% Bước 3: xây dựng biến và điều kiện biên
u = sym('u', [n+1, m+1])

for i = 1:n+1
    u(i, 1) = g(X(i), Y(1));
    u(i, m+1) = g(X(i), Y(m+1));
end
for j = 1:m+1
    u(1, j) = g(X(1), Y(j));
    u(n+1, j) = g(X(n+1), Y(j));
end

% Bước 4: đánh chỉ số tuyến tính các biến
p = sym('p', [(n-1)*(m-1), 1])
for i = 2:n
    for j = 2:m
        u(i, j) = p((n-1) * (j-2) + i-1)
    end
end

% Bước 5: xây dựng hệ phương trình
for j = 2:m
    for i = 2:n
        -2 * ((h/k)^2 + 1) * u(i, j) + u(i-1, j) + u(i+1, j) + (h/k)^2 * (u(i, j-1) + u(i, j+1)) - h^2 * f(X(i+1), Y(j+1))
    end
end

% Bước 6: (tự làm) hệ phương trình dạng ma trận
% Bước 7: (tự làm) giải hệ ở bước 6

% Bonus: giải hệ ở bước 5
eqns = sym('e', [(n-1)*(m-1), 1])
for j = 2:m
    for i = 2:n
        eqns((n-1) * (j-2) + i-1) = -2 * ((h/k)^2 + 1) * u(i, j) + u(i-1, j) + u(i+1, j) + (h/k)^2 * (u(i, j-1) + u(i, j+1)) - h^2 * f(X(i+1), Y(j+1));
    end
end
eqns

sol = solve(eqns)

sol.p3  % thay 3 từ 1 tới 21 = (n-1)(m-1)

% Bước 1: Khai báo g

function val = g(x, y)
if y == 0
    val = x^2;
end
if y == 2
    val = (x-2)^2;
end
if x == 0
    val = y^2;
end
if x == 1
    val = (y-1)^2;
end
end
```
