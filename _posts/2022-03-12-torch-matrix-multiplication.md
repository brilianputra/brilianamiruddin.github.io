﻿---
layout: post
toc: true
title: "[PyTorch/파이토치 기초] matmul, mm, and bmm"
categories: study-log
tags: [machine-learning, pytorch]
author:
  - Brilian Putra Amiruddin
---

<a href="https://colab.research.google.com/drive/1i-xscoArLfV3qjUSFpPyRA3uykBi-C0x#scrollTo=orcx_gB85JBl">  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

In general, ``PyTorch`` has 3 different types of matrix multiplication and each of the types has its own characteristics and the way to use it. They are ``torch.matmul, torch.mm, and torch.bmm``. Then, let’s look at them one by one in detail!. 

파이토치는 3종 행렬 곱셈이 기본적으로 가지고 있으며 각각 종은 다른 특징과 방식도 갖는다. 그것들은 ``torch.matmul, torch.mm, torch.bmm``. 그렇다면, 각각 행렬 곱셈의 기능에 대해 상세하게 알아보자!.

## torch.matmul

The ``torch.matmul`` has an ability to perform the matrix multiplication in several ways. This ``torch.matmul`` can automatically broadcast the tensor size to fit the the other tensor sizes without explicitly define the compatible tensor sizes during multiplication. Additionally, ``torch.matmul`` is also able to perform matrix with scalar multiplication, vanilla matrix multiplications, and batched matrix multiplication.

``torch.matmul``은 몇 몇 행렬 곱셈의 기능을 갖는다. 텐서의 크기가 맞을 수 있도록 이 ``torch.matmul``이 자동적으로 텐서를 broadcast할 수 있으며 텐서의 크기를 스스로 정의하는 것이 필요없다. 게다가, ``torch.matmul``도 행렬과 스칼라 곱셈, 평범한 행렬 곱셈, 그리고 배치 행렬 곱셈이다.
> torch.matmul 구현 코드

```python
# 1D (3) tensor x 1D (3) tensor
a = torch.rand(3)
b = torch.rand(3)
print(torch.matmul(a,b).size())
# The output is 0D ([]) tensor (scalar)

# 2D (3,3) tensor x 1D (3) broadcasted tensor
a = torch.rand(3,3)
b = torch.rand(3)
print(torch.matmul(a,b).size())
# The output is 1D ([3]) tensor (vector)

# 2D (3,3) tensor x 2D (3x3) tensor
a = torch.rand(3,3)
b = torch.rand(3,3)
print(torch.matmul(a,b).size())
# The output is 2D ([3,3]) tensor (matrix)

# 3D (3,1,2) tensor (batched matrix) x 1D (2) broadcasted tensor
a = torch.rand(3,1,2)
b = torch.rand(2)
print(torch.matmul(a,b).size())
# The output is 2D ([3,1]) tensor

# 3D (3,1,2) tensor (batched matrix) x 3D (3,2,3) batched matrix
a = torch.rand(3,1,2)
b = torch.rand(3,2,3)
print(torch.matmul(a,b).size())
# The output is 3D ([3,1,3]) tensor
``` 
## torch.mm

``torch.mm`` function is only used for multiplying 2D tensor or we can say to perform a vanilla 2D matrix multiplication. Different with ``torch.matmul`` the ``torch.mm`` function doesn’t have tensor broadcasting ability.

``torch.mm``은 2D 텐서를 곱셈하기 위하거나 평범한 2D 행렬 곱셈을 사용한다. ``torch.matmul``과 ``torch.mm``이  다른 점은 텐서 broadcasting 기능을 갖지 않는다.  

> torch.mm 구현 코드

```python
# Vanilla matrix multiplication (tensor 2D) (2,3) x (3,10)
a = torch.rand(2,3)
b = torch.rand(3,10)
print(torch.mm(a,b).size())
# The matrix output size is (2,10) => (n, m) * (m, a) = (n, a)
```


## torch.bmm
The last one is ``torch.bmm``, this function is only for doing batched tensor multiplication. However, compared to the ``torch.matmul``, the ``torch.bmm`` also doesn’t have ability to do tensor broadcasting. Therefore, ``torch.bmm`` is merely a special function for doing batched tensor multiplication.

마지막으로, ``torch.bmm``이다, 이 기능은 배치 텐서 곱셈을 할 수 밖에 없다. 그렇지만, ``torch.matmul``에 비해 ``torch.bmm``도 텐서 broadcasting 기능을 가지지 않는다. 따라서 ``torch.bmm``은 특별한 배치 텐서를 하기 위한 기능일 뿐이다. 

> torch.bmm 구현 코드

```python
# Batched tensor multiplication
a = torch.rand(3,1,2)
b = torch.rand(3,2,4)
print(torch.bmm(a,b).size())
# The output size is (3,1,4)
```

> Written with [StackEdit](https://stackedit.io/) ❤️.
