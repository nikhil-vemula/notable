---
title: Octave
created: '2020-12-01T15:57:47.287Z'
modified: '2020-12-01T16:31:12.347Z'
---

# Octave

## Basic operations

```octave
1/2
1==2
1~=2 % Not equals
a=1; disp(a)

% Matrices
A = [1 2; 3 4; 5 6]
V = 1:0.1:2
2*ones(2,3)
w = rand(1,3)
eye(4)

hist(w) % Histrogram
```

## Moving data around

```
size(A)
size(A, 1)

load filename
who % List all variables
```

## Computing

```
A .* B % Element wise
A'
max(A)
```

## Plotting

```
plot()
hold on;
```
