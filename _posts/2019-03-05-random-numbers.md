---
layout: post
title:  "Numeros aleatórios"
date:	2019-03-05 16:53:00 -0200
subtitle: "Investigando os métodos para gerar números aleatórios"
Comments: true
categories: "math, fundamentals, computation"
---

## Aplicações

Números aleatórios são utilizados em uma grande gama de aplicações como:

- Simulação de eventos naturais;
- Sampling criação de datasets dentro de populações de dados;
- Análise numérica;
- Teste de efetividade de algorítimos;
- Tomadas de decisões não enviesadas;
- Criptografia com a geração de bits não enviesados;
- Estética com um pouco de aleatoriedade em gráficos e musicas geradas;
- Recreação com dados, cartas, roletas e etc;

## Background

- 40000 Random digits 1927 L.H.C. Tippet

- 100000 Random numbers 1939 M.G. Kendal an B. Babinton

- Ferrati Mark 1951 gerava numeros aleatórios através de uma maquina de resistências elétricas (Turing)

- RAND Corporation

- ERNIE British lottery

- Jhon von Newmann 1946 - Quadrado do numero anterior (middle square)

### Métodos

### Linear Congruential method

$$
Xn+1= (aXn+c)mod m
$$

### Additive Number generator

### Inverse congruential sequence

### Randomizing by shuffling

## Sequencias suficientimente aleatórias

### Métodos de verificação

- General test procedures
- Empirical tests
- Theorical tests
- Spectral test

## Gerador de aleatórios em C

```c
/* If we are using the trivial TYPE_0 R.N.G., just do the old linear
   congruential bit.  Otherwise, we do our fancy trinomial stuff, which is the
   same in all the other cases due to all the global variables that have been
   set up.  The basic operation is to add the number at the rear pointer into
   the one at the front pointer.  Then both pointers are advanced to the next
   location cyclically in the table.  The value returned is the sum generated,
   reduced to 31 bits by throwing away the "least random" low bit.
   Note: The code takes advantage of the fact that both the front and
   rear pointers can't wrap on the same call by not testing the rear
   pointer if the front one has wrapped.  Returns a 31-bit random number.  */

int
__random_r (struct random_data *buf, int32_t *result)
{
  int32_t *state;

  if (buf == NULL || result == NULL)
    goto fail;

  state = buf->state;

  if (buf->rand_type == TYPE_0)
    {
      int32_t val = ((state[0] * 1103515245U) + 12345U) & 0x7fffffff;
      state[0] = val;
      *result = val;
    }
  else
    {
      int32_t *fptr = buf->fptr;
      int32_t *rptr = buf->rptr;
      int32_t *end_ptr = buf->end_ptr;
      uint32_t val;

      val = *fptr += (uint32_t) *rptr;
      /* Chucking least random bit.  */
      *result = val >> 1;
      ++fptr;
      if (fptr >= end_ptr)
	{
	  fptr = state;
	  ++rptr;
	}
      else
	{
	  ++rptr;
	  if (rptr >= end_ptr)
	    rptr = state;
	}
      buf->fptr = fptr;
      buf->rptr = rptr;
    }
  return 0;

 fail:
  __set_errno (EINVAL);
  return -1;
}

weak_alias (__random_r, random_r)
```
