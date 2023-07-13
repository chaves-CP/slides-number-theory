<section id="themes">
	<h2>Themes</h2>
		<p>
			Set your presentation theme: <br>
			<!-- Hacks to swap themes after the page has loaded. Not flexible and only intended for the reveal.js demo deck. -->
                        <a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/black.css'); return false;">Black (default)</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/white.css'); return false;">White</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/league.css'); return false;">League</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/sky.css'); return false;">Sky</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/beige.css'); return false;">Beige</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/simple.css'); return false;">Simple</a> <br>
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/serif.css'); return false;">Serif</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/blood.css'); return false;">Blood</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/night.css'); return false;">Night</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/moon.css'); return false;">Moon</a> -
			<a href="#" onclick="document.getElementById('theme').setAttribute('href','css/theme/solarized.css'); return false;">Solarized</a>
		</p>
</section>

H:

# Teoria de Números [Inicial]

by Sebastian Chaves  
[![Linkedin](fig/icons8-linkedin-48.png)](https://www.linkedin.com/in/jschavesr/) 
[![Github](fig/icons8-github-48.png)](https://github.com/jschavesr) 
[![Codeforces](fig/icons8-codeforces-48.png)](https://codeforces.com/profile/Chaves) 

[Training Camp Medellin](https://www.tcmedellin.com/) 



Disponible en: [chaves-cp.github.io/slides-number-theory](https://chaves-cp.github.io/slides-number-theory)   


H:

# Indice

1. Teoria de Numeros<!-- .element: class="fragment" data-fragment-index="1"-->
	* Números primos
	* Aritmetica Modular


H:
## Número Primo

> Número natural mayor o igual a 2 tal que es divisible por 1 y por él mismo

Ejemplo: 2, 5, 7, 10^9 + 7 :D

V:

## Descomposicion en factores primos

> Todo número natural se puede expresar como forma de producto de factores primos

Ejemplo:

18 = 2 * 3^2
24 = 2^3 * 3


V:

## Algunas preguntas

* ¿Cómo sé si un número es primo?<!-- .element: class="fragment" data-fragment-index="1"-->
* ¿Cuál es el i-esimo número primo?<!-- .element: class="fragment" data-fragment-index="2"-->
* ¿Cuántos números primos hay entre 1 y n?<!-- .element: class="fragment" data-fragment-index="3"-->

V: 
## Prueba de primalidad

```cpp
	bool isPrime(int x) {
		if (x < 2) return false;
		for (int i=2; i<x; i++) 
			if (x % i == 0) return false;
		return true;
	}
```


V: 
## Prueba de primalidad, mejorada?

> X es primo si no tiene divisores entre 2 y sqrt(N)<!-- .element: class="fragment"-->

```cpp
#include <iostream>

using namespace std;

bool isPrimeV2(int x) {
	if (x < 2) return false;
	for (int i=2; i*i<=x; i++) 
		if (x % i == 0) return false;
	return true;
}
```
<!-- .element: class="fragment"-->

V: 

## Prueba de primalidad mejor que la mejorada

> Revisar solo factores primos entre 2 y sqrt(N) <!-- .element: class="fragment"-->


> ¿Cómo encuentro cuales son los números primos? <!-- .element: class="fragment"-->

V:
## Criba de Eratóstenes

>  [Algoritmo](https://es.wikipedia.org/wiki/Criba_de_Erat%C3%B3stenes) que permite hallar todos los números primos menores que un número natural dado.

<figure>
    <img height='400' src='fig/Sieve_of_Eratosthenes_animation.gif' />
</figure>

V: 

## Codigo

```cpp
#include <bits/stdc++.h>
ll _sieve_size; // ll is defined as: typedef long long ll;
bitset<10000010> bs; // 10^7 should be enough for most cases
vector<int> primes; 
void sieve(ll upperbound) { // create list of primes in [0..upperbound]
	_sieve_size = upperbound + 1; // add 1 to include upperbound
	bs.set(); // set all bits to 1
	bs[0] = bs[1] = 0; // except index 0 and 1
	for (ll i = 2; i <= _sieve_size; i++) {
		if (bs[i]) {// cross out multiples of i starting from i * i!
			for (ll j = i * i; j <= _sieve_size; j += i) bs[j] = 0;
				primes.push_back((int)i); // add this prime to the list of primes
			} 
	} // call this method in main method
}
```

V: 

## Ahora si la versión mejor mejorada

```cpp
bool isPrime(ll N) { // a good enough deterministic prime tester
	if (N <= _sieve_size) return bs[N]; // O(1) for small primes
	for (int i = 0; i < (int)primes.size(); i++)
		if (N % primes[i] == 0) return false;
	return true; // it takes longer time if N is a large prime!
} // note: only work for N <= (last prime in vi "primes")^2

```

V: 
## Hay algo mejor?

Sí <!-- .element: class="fragment"-->


Lo vamos a ver?<!-- .element: class="fragment"-->

No <!-- .element: class="fragment"-->

Pero si tienen curiosidad: <!-- .element: class="fragment"-->
 [Miller–Rabin primality test](https://en.wikipedia.org/wiki/Miller%E2%80%93Rabin_primality_test#:~:text=The%20Miller%E2%80%93Rabin%20primality%20test,the%20Solovay%E2%80%93Strassen%20primality%20test.)<!-- .element: class="fragment"-->




V:
## Primos relativos


> Dos números enteros positivos son primos relativos si no tienen ningún factor primo en común;


V:
## Máximo Cómun Divisor (gcd) y Minimo Común Múltiplo(lcm)

```cpp
	int gcd(int a, int b) { return b == 0 ? a : gcd(b, a % b); }
	int lcm(int a, int b) { return a * (b / gcd(a, b)); }


	// Also you can use __gcd function from cpp
	// int ans = __gcd(x, y)
```

H:

## Aritmetica modular



V:

## Cómo calcular el factorial de un numero? 

```cpp
int fact[100];
void calculateFact() {
	fact[0] = 1;
	for (int i=1; i<100; i++) fact[i] = i * fact[i-1]

	return;
}
``` 

Pero el factorial de 15! tiene 12 digitos


V: 


## Cómo calcular el factorial de un numero? 

```cpp
int fact[100];
const int MOD = 10007;
void calculateFact() {
	fact[0] = 1;
	for (int i=1; i<100; i++) (fact[i] = i * fact[i-1]) % MOD;

	return;
}
``` 
Ahora todos los numeros estan entre 0 y 10007;

V:

## Propiedades armetica modular

* (a + b) % c = a % c + b % c <!-- .element: class="fragment"-->
* (a - b) % c = a % c - b % c <!-- .element: class="fragment"-->
* (a \* b) % c = a % c \* b % c <!-- .element: class="fragment"-->

 Y la division? <!-- .element: class="fragment"-->



V:
## Congruencia 

> a y b se encuentran en la misma "clase de congruencia" módulo n, si ambos dejan el mismo resto si los dividimos entre n, o, equivalentemente, si a − b es un múltiplo de n.



> 63 es congruente a 83 modulo 10 y se escribe 63 ≡ 83 (mod 10) 

> a  ≡ b (mod N)

V:
## Inverso modular

> a y b son inversos modulares si a * b  ≡ 1 (mod M)

> A^-1 es el inverso modular de A (solo en terminos de notacion)

V:

## Pequeño teorema de fermat

[Link](https://es.wikipedia.org/wiki/Peque%C3%B1o_teorema_de_Fermat)


> Lo importante es que el inverso modular (modulo p ) de A es A^(p-1)

V::

## Fast Pow 

```cpp
const long long MOD = 1e9 + 7;
long long fastPow(long long a, long long b) {
	if (b == 0) return 1ll;
	if (b == 1) return a;
	if (b % 2 == 0) {
		long long tmp = fastPow(a, b/2);
		return (tmp * tmp) % MOD;
	} 

	return (a * fastPow(a, b-1)) % MOD
}
```


V:

## El código que yo uso para aritmetica modular

```cpp
using ll = long long;
ll modinv(ll a, ll m) {
	assert(m > 0);
	if (m == 1) return 0;
	a %= m;
	if (a < 0) a += m;
	assert(a != 0);
	if (a == 1) return 1;
	return m - modinv(m, a) * m / a;
}

template <int MOD_> struct modnum {
private:
	int v;
public:
	static const int MOD = MOD_;
 
	modnum() : v(0) {}
	modnum(ll v_) : v(int(v_ % MOD)) { if (v < 0) v += MOD; }
	explicit operator int () const { return v; }
	friend bool operator == (const modnum& a, const modnum& b) { return a.v == b.v; }
	friend bool operator != (const modnum& a, const modnum& b) { return a.v != b.v; }
 
	modnum operator ~ () const {
		modnum res;
		res.v = modinv(v, MOD);
		return res;
	}
 
	modnum& operator += (const modnum& o) {
		v += o.v;
		if (v >= MOD) v -= MOD;
		return *this;
	}
	modnum& operator -= (const modnum& o) {
		v -= o.v;
		if (v < 0) v += MOD;
		return *this;
	}
	modnum& operator *= (const modnum& o) {
		v = int(ll(v) * ll(o.v) % MOD);
		return *this;
	}
	modnum& operator /= (const modnum& o) {
		return *this *= (~o);
	}
 
	friend modnum operator + (const modnum& a, const modnum& b) { return modnum(a) += b; }
	friend modnum operator - (const modnum& a, const modnum& b) { return modnum(a) -= b; }
	friend modnum operator * (const modnum& a, const modnum& b) { return modnum(a) *= b; }
	friend modnum operator / (const modnum& a, const modnum& b) { return modnum(a) /= b; }
};
 
using num = modnum<int(1e9) + 7>;
 
vector<num> fact;
vector<num> ifact;
 
void init(){
	fact = {1};
	for(int i = 1; i < 100000; i++) fact.push_back(i * fact[i-1]);
	for(num x : fact) ifact.push_back(1 / x);	
}
 
num ncr(int n, int k){
	if(k < 0 || k > n) return 0;
	return fact[n] * ifact[k] * ifact[n-k];
}
 
num powmod(num x, ll a){
	if(a == 0) return 1;
	if(a & 1) return x * powmod(x, a-1);
	return powmod(x * x, a/2);
}
```
 






