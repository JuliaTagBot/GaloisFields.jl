# GaloisFields.jl - finite fields for Julia

## Introduction

This module defines types representing [finite fields][galois-fields-wiki]. It
supports both fields of prime order and of prime power order.

The module makes no attempt to verify that you pass a prime characteristic,
or that the minimum polynomial is irreducible. The caller is responsible
for that.

[galois-fields-wiki]: https://en.wikipedia.org/wiki/Finite_field

## Synopsis

```julia
using GaloisFields
F = GaloisField(3)
F = @GaloisField ℤ/3ℤ
F = @GaloisField 𝔽₃

F, β = GaloisField(3, :β => [2, 1, 1])
F = @GaloisField! 𝔽₃ β^2 + β + 2

F(1) + F(2) == 0
β^2 + β + 2 == 0
```

## Non-canonical identifications
In the case of extension fields, the variable name (e.g. β above) is part of the
type. This lets you define identifications between isomorphic (sub)fields. For
example, with the following definition

```julia
F = @GaloisField! 𝔽₂ β^2 + β + 1
G = @GaloisField! 𝔽₂ γ^2 + γ + 1
```

the fields ``F`` and ``G`` are isomorphic, but not canonically. We might
define

```julia
@GaloisFields.identify β => γ + 1
@GaloisFields.identify γ => β + 1
```

to allow for conversions like

```julia
G(β)
convert(F, γ + 1)
```
