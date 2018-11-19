---
id: 1737
title: '5.6 Integração Numérica &#8212; Quadratura de Gauss'
date: 2012-08-07T19:56:15+00:00
author: SAWP
excerpt: Quadratura de Gauss é um método de integração numérica também chamado de quadratura gaussiana ou quadratura de Legendre.
layout: post
guid: http://www.sawp.com.br/blog/?p=1737
permalink: p=1737
wp-syntax-cache-content:
  - |
    a:7:{i:1;s:3260:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> compute_legendre_polynomials_coeficients<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Compute the coefficients of the nth Legendre polynomial.
    &nbsp;
    [coefficients] = compute_legendre_polynomials_coeficients(n)
    &nbsp;
    INPUT:
    * n: order of the Legendre polynomial
    &nbsp;
    return: a list containing the polynomial coefficients of nth Legendre
    polynomial (ordered from the highest to lowest)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    b <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2.0</span> ** n
    B <span style="color: #66cc66;">=</span> binomial_coefficients
    f <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> k: b * B<span style="color: black;">&#40;</span>n<span style="color: #66cc66;">,</span> k<span style="color: black;">&#41;</span> * B<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>n + k - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2.0</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>
    a <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>f<span style="color: black;">&#40;</span>k<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> n + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    a.<span style="color: black;">reverse</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> a</pre></td></tr></table><p class="theCode" style="display:none;">def compute_legendre_polynomials_coeficients(n):
    &quot;&quot;&quot;
    Compute the coefficients of the nth Legendre polynomial.
    
    [coefficients] = compute_legendre_polynomials_coeficients(n)
    
    INPUT:
    * n: order of the Legendre polynomial
    
    return: a list containing the polynomial coefficients of nth Legendre
    polynomial (ordered from the highest to lowest)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    b = 2.0 ** n
    B = binomial_coefficients
    f = lambda k: b * B(n, k) * B((n + k - 1) / 2.0, n)
    a = [f(k) for k in xrange(0, n + 1)]
    a.reverse()
    return a</p></div>
    ;i:2;s:2740:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> binomial_coefficients<span style="color: black;">&#40;</span>n<span style="color: #66cc66;">,</span> k<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Calcule any binomial coefficients.
    &nbsp;
    coeff = binomial coefficients(n, k)
    &nbsp;
    INPUT:
    * n: power of binomial
    * k: coefficient of x^k term
    &nbsp;
    return: binomial coefficient
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    fun <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> i: <span style="color: black;">&#40;</span>n - i + <span style="color: #ff4500;">1.0</span><span style="color: black;">&#41;</span> / i
    l <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">1.0</span><span style="color: black;">&#93;</span> + <span style="color: black;">&#91;</span>fun<span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> k + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    coeff <span style="color: #66cc66;">=</span> <span style="color: #008000;">reduce</span><span style="color: black;">&#40;</span>mul<span style="color: #66cc66;">,</span> l<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> coeff</pre></td></tr></table><p class="theCode" style="display:none;">def binomial_coefficients(n, k):
    &quot;&quot;&quot;
    Calcule any binomial coefficients.
    
    coeff = binomial coefficients(n, k)
    
    INPUT:
    * n: power of binomial
    * k: coefficient of x^k term
    
    return: binomial coefficient
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    fun = lambda i: (n - i + 1.0) / i
    l = [1.0] + [fun(i) for i in xrange(1, k + 1)]
    coeff = reduce(mul, l)
    return coeff</p></div>
    ;i:3;s:2795:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> compute_legendre_roots<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Compute all roots of the nth Legendre polynomial
    &nbsp;
    [roots] = compute_legendre_roots(n)
    &nbsp;
    INPUT:
    * n: order of Legendre polynomial
    &nbsp;
    return: the roots of P_n(x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    legendre_coefficients <span style="color: #66cc66;">=</span> compute_legendre_polynomials_coeficients<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>
    diff_coefs <span style="color: #66cc66;">=</span> polynomial_derivative_coefficients<span style="color: black;">&#40;</span>legendre_coefficients<span style="color: black;">&#41;</span>
    legendre_fun <span style="color: #66cc66;">=</span> polynomial_coeffs_to_function<span style="color: black;">&#40;</span>legendre_coefficients<span style="color: black;">&#41;</span>
    diff_legendre_fun <span style="color: #66cc66;">=</span> polynomial_coeffs_to_function<span style="color: black;">&#40;</span>diff_coefs<span style="color: black;">&#41;</span>
    roots <span style="color: #66cc66;">=</span> aberth<span style="color: black;">&#40;</span>legendre_fun<span style="color: #66cc66;">,</span> diff_legendre_fun<span style="color: #66cc66;">,</span> polDegree<span style="color: #66cc66;">=</span>n<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> roots</pre></td></tr></table><p class="theCode" style="display:none;">def compute_legendre_roots(n):
    &quot;&quot;&quot;
    Compute all roots of the nth Legendre polynomial
    
    [roots] = compute_legendre_roots(n)
    
    INPUT:
    * n: order of Legendre polynomial
    
    return: the roots of P_n(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    legendre_coefficients = compute_legendre_polynomials_coeficients(n)
    diff_coefs = polynomial_derivative_coefficients(legendre_coefficients)
    legendre_fun = polynomial_coeffs_to_function(legendre_coefficients)
    diff_legendre_fun = polynomial_coeffs_to_function(diff_coefs)
    roots = aberth(legendre_fun, diff_legendre_fun, polDegree=n)
    return roots</p></div>
    ;i:4;s:2808:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> polynomial_derivative_coefficients<span style="color: black;">&#40;</span>coeff<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Compute the derivative of a polynomial represented by a list.
    &nbsp;
    [diff_coefficients] = polynomial_derivative_coefficients(coeff)
    &nbsp;
    INPUT:
    * coeff: coefficients of the polynomial
    &nbsp;
    return: a list containing the polynomial coefficients of the derivated
    polynomial (ordered from the highest to lowest)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    order <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>coeff<span style="color: black;">&#41;</span> - <span style="color: #ff4500;">1</span>
    f <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> i: <span style="color: black;">&#40;</span>order - i<span style="color: black;">&#41;</span> * coeff<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    diff <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>f<span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>order<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> diff</pre></td></tr></table><p class="theCode" style="display:none;">def polynomial_derivative_coefficients(coeff):
    &quot;&quot;&quot;
    Compute the derivative of a polynomial represented by a list.
    
    [diff_coefficients] = polynomial_derivative_coefficients(coeff)
    
    INPUT:
    * coeff: coefficients of the polynomial
    
    return: a list containing the polynomial coefficients of the derivated
    polynomial (ordered from the highest to lowest)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    order = len(coeff) - 1
    f = lambda i: (order - i) * coeff[i]
    diff = [f(i) for i in xrange(order)]
    return diff</p></div>
    ;i:5;s:2567:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> polynomial_coeffs_to_function<span style="color: black;">&#40;</span>coeff<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Convert the polynomial coefficients in a polynomial function.
    &nbsp;
    function = polynomial_coeffs_to_function(coeff)
    &nbsp;
    INPUT:
    * coeff: coefficients of the polynomial
    &nbsp;
    return: a function
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    order <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>coeff<span style="color: black;">&#41;</span> - <span style="color: #ff4500;">1</span>
    f <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> x: <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span>coeff<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> * x ** <span style="color: black;">&#40;</span>order - i<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>order + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> f</pre></td></tr></table><p class="theCode" style="display:none;">def polynomial_coeffs_to_function(coeff):
    &quot;&quot;&quot;
    Convert the polynomial coefficients in a polynomial function.
    
    function = polynomial_coeffs_to_function(coeff)
    
    INPUT:
    * coeff: coefficients of the polynomial
    
    return: a function
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    order = len(coeff) - 1
    f = lambda x: sum([coeff[i] * x ** (order - i) for i in xrange(order + 1)])
    return f</p></div>
    ;i:6;s:4595:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> compute_quadrature_weights<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Compute the weights of each coefficient used in gaussian quadrature.
    &nbsp;
    [weights] = compute_quadrature_weights(n)
    &nbsp;
    INPUT:
    * n: order of Legendre polynomial
    &nbsp;
    return: a list with the weights
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> get_diff_Legendre_n<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    l1 <span style="color: #66cc66;">=</span> compute_legendre_polynomials_coeficients<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>
    diff_coefs <span style="color: #66cc66;">=</span> polynomial_derivative_coefficients<span style="color: black;">&#40;</span>l1<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> polynomial_coeffs_to_function<span style="color: black;">&#40;</span>diff_coefs<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> compute_weights<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    p1n <span style="color: #66cc66;">=</span> get_diff_Legendre_n<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>
    a <span style="color: #66cc66;">=</span> compute_legendre_roots<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> i: <span style="color: #ff4500;">2.0</span> / <span style="color: black;">&#40;</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1.0</span> - a<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> * a<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> * p1n<span style="color: black;">&#40;</span>a<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> * p1n<span style="color: black;">&#40;</span>a<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    H <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>h<span style="color: black;">&#40;</span>j<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> H
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> compute_weights<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def compute_quadrature_weights(n):
    &quot;&quot;&quot;
    Compute the weights of each coefficient used in gaussian quadrature.
    
    [weights] = compute_quadrature_weights(n)
    
    INPUT:
    * n: order of Legendre polynomial
    
    return: a list with the weights
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    def get_diff_Legendre_n(n):
    l1 = compute_legendre_polynomials_coeficients(n)
    diff_coefs = polynomial_derivative_coefficients(l1)
    return polynomial_coeffs_to_function(diff_coefs)
    
    def compute_weights(n):
    p1n = get_diff_Legendre_n(n)
    a = compute_legendre_roots(n)
    h = lambda i: 2.0 / ((1.0 - a[i] * a[i]) * p1n(a[i]) * p1n(a[i]))
    H = [h(j) for j in xrange(n)]
    return H
    
    return compute_weights(n)</p></div>
    ;i:7;s:5455:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> integral_gaussian_quadrature<span style="color: black;">&#40;</span>fun<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> order<span style="color: #66cc66;">=</span><span style="color: #ff4500;">10</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration using Gaussian quadrature
    &nbsp;
    integral = integral_gaussian_quadrature(fun, xi, xe, order=10)
    &nbsp;
    INPUT:
    * fun: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * order: degree of Legendre polynomial
    &nbsp;
    return: <span style="color: #000099; font-weight: bold;">\i</span>nt_{xi}^{xe} f(x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> convert_intervals<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    frac <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2.0</span>
    xd <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> x: <span style="color: black;">&#40;</span>xe + xi + <span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> * x<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2.0</span>
    f <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> x: fun<span style="color: black;">&#40;</span>xd<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> * frac
    <span style="color: #ff7700;font-weight:bold;">return</span> f
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> compute_quadrature<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    f <span style="color: #66cc66;">=</span> convert_intervals<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    roots <span style="color: #66cc66;">=</span> compute_legendre_roots<span style="color: black;">&#40;</span>order<span style="color: black;">&#41;</span>
    weights <span style="color: #66cc66;">=</span> compute_quadrature_weights<span style="color: black;">&#40;</span>order<span style="color: black;">&#41;</span>
    approx <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> i: weights<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> * f<span style="color: black;">&#40;</span>roots<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>.<span style="color: black;">real</span><span style="color: black;">&#41;</span>
    quad <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>approx<span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>order<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span>quad<span style="color: black;">&#41;</span>
    &nbsp;
    integral <span style="color: #66cc66;">=</span> compute_quadrature<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> integral</pre></td></tr></table><p class="theCode" style="display:none;">def integral_gaussian_quadrature(fun, xi, xe, order=10):
    &quot;&quot;&quot;
    Numerical integration using Gaussian quadrature
    
    integral = integral_gaussian_quadrature(fun, xi, xe, order=10)
    
    INPUT:
    * fun: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * order: degree of Legendre polynomial
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    def convert_intervals():
    frac = (xe - xi) / 2.0
    xd = lambda x: (xe + xi + (xe - xi) * x) / 2.0
    f = lambda x: fun(xd(x)) * frac
    return f
    
    def compute_quadrature():
    f = convert_intervals()
    roots = compute_legendre_roots(order)
    weights = compute_quadrature_weights(order)
    approx = lambda i: weights[i] * f(roots[i].real)
    quad = [approx(i) for i in xrange(order)]
    return sum(quad)
    
    integral = compute_quadrature()
    return integral</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 



Consideremos o problema de encontrar uma aproximação numérica \(I(f) \) para a integral da função linear \(f(x) \)
  


<center>
  \( I(f) = \int_a^b f(x) dx \)
</center>


  
onde \(-\infty \leq a \leq b \infty \) . Como \(I(f) \) é linear. É coerente aproximarmos isso por um funcional também linear,
  


<center>
  \( Q(f) = \sum_{i=0}^m \sum_{j=1}^n A_{ij} f^{(i)}(a_{ij}) \)
</center>


  
onde \(Q(f) \) é chamada de _problema da quadratura_. Isto é,

<center>
  \( I(f) = Q(f) + E \)
</center>


  
Note que quando \(E=0 \) , temos a aproximação da integral como uma combinação linear dos valores de \(f(x) \) e suas derivadas. O problema da quadratura numérica consiste em especificar \(A\_{ij} \) e \(a\_{ij} \) tais que esta aproximação obedeçam a certas propriedades, tais como convergência e acurácia. 

Nossa abordagem consiste em definir uma aproximação polinomial de \(f(x) \) de forma a escolher \(A\_{ij} \) e \(a\_{ij} \) tais que minimizem \(E \) para um aproximante de grau suficientemente baixo. Assim como fizemos com a regra do trapézio, representaremos a integral como uma combinação linear de valores funcionais
  
únicos. Ou seja, reescreveremos a integral como
  


<center>
  \( \int_a^b f(x) dx = \sum_{j=1}^{n} H_j f(a_j) + E \)
</center>

Vamos assumir que os limites de integração \(a \) e \(b \) da equação acima são finitos. Se a equação acima é exata para polinômios de grau \(2n-1 \) ou menores, podemos utilizar um conjunto de \(2n \) equações para descobrir \(2n \) constantes ao substituir \(f(x) = x^k \) para \(k=0,1,\ldots,2n-1 \) na equação acima. Setando \(E=0 \) , temos que
  


<center>
  \( \alpha_k = \sum_{j=1}^{n} H_j a_j^k \)
</center>


  
para \(k=0,1,\ldots,2n-1 \) , onde
  


<center>
  \( \alpha_k = \int_a^b x^k dx = \frac{b^{k+1} &#8211; a^{k+1}}{k+1} \)
</center>

Seja a fórmula de interpolação de Hermite:
  


<center>
  \( f(x) = \sum_{j=1}^n h_j f(a_j) + \sum_{j=1}^n \hat{h_j(x)} f'(a_j) + \frac{pn^2(x)}{(2n)!} f^{(2n)}(\xi) \)
</center>


  
que é exata para os polinômios de grau \(2n-1 \) ou menores. Integrando essa equação, temos
  


<center>
  \( \int_a^b f(x) dx = \sum_{j=1}^n H_j f(a_j) + \sum_{j=1}^n \hat{H_j} f'(a_j) + E \)
</center>


  
onde
  


<center>
  \( H_j = \sum_a^b h_j(x) dx \)
</center>


  
e
  


<center>
  \( \hat{H_j} = \int_a^b \hat{h_j}(x) dx \)
</center>


  
Como \(E \) é zero, se \(f(x) \) é um polinômio de grau \(2n-1 \) ou menor e se podemos escolher as abcissas tal que \(\hat{H_j} = 0 \) , então teremos as propriedades desejadas. 

&nbsp;

## 2. Quadratura de Gauss-Legendre 



A quadratura de Gauss-Legendre consiste em aproximar a integral \(I(f) \) utilizando \(n \) pontos
  


<center>
  \( I(f) = H_0 f(a_0) + H_1 f(a_1) + \cdots + H_{n-1} f(a_{n-1}) \)
</center>


  
onde as abcissas \(a_j \) são as raízes do polinômio de Legendre e os pesos são obtidos por

<center>
  \( H_j = \dfrac{-2}{(n+1) P_{n+1}(a_j)P&#8217;_n(a_j)} = \dfrac{2}{(1-a_j^2) P&#8217;_n(a_j)} \)
</center>



## 3. Implementação 



Como podemos notar das seções anteriores, a quadratura requer avaliar a função em pontos bem definidos utilizando pesos específicos. Como dito na última seção, os pontos a serem utilizados \(a\_j \) são as raízes do polinômio de Legendre. Além disso, podemos ver que os pesos também dependem dessas raízes \(a\_j \) . Sendo assim, o problema da quadratura de Gauss-Legendre é resolvido em resolver quatro grandes etapas:

  1. Obter o polinômio de Legendre de ordem \(n \) , onde \(n \) é o número de pontos utilizados. 
  2. Encontrar as \(n \) raízes do polinômio obtido. 
  3. Encontrar a primeira derivada do n-ésimo polinômio, pois o peso é dependente desta função. Com isso podemos determinar os pesos \(H_j \) . 
  4. Computar a quadratura gaussiana, utilizando os pesos \(H\_j \) e as raízes \(a\_j \) . 

&nbsp;

### 3.1. Computando o Polinômio de Legendre 

O primeiro passo é encontrar os polinômios de Legendre para que possamos encontrar suas raízes. Como sabemos que nos passos posteriores teremos que encontrar a derivada do n-ésimo polinômio, escolhemos gerar seus coeficientes e colocá-los em uma lista ordenada da maior ordem para a menor. Por exemplo, o polinômio
  


<center>
  \( p(x) = 3x^4 + 2x^3 &#8211; x + 7 \)
</center>


  
pode ser representado em forma de lista
  


<center>
  \( p(x) = [3, 2, 0, -1, 7] \)
</center>


  
onde a ordem fica implícita na posição do vetor em ordem decrescente. Assim, a função que computa os coeficientes, representando o polinômio como uma lista é

<pre lang="python">def compute_legendre_polynomials_coeficients(n):
    """
    Compute the coefficients of the nth Legendre polynomial.

    [coefficients] = compute_legendre_polynomials_coeficients(n)

    INPUT:
      * n: order of the Legendre polynomial

    return: a list containing the polynomial coefficients of nth Legendre
            polynomial (ordered from the highest to lowest)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    b = 2.0 ** n
    B = binomial_coefficients
    f = lambda k: b * B(n, k) * B((n + k - 1) / 2.0, n)
    a = [f(k) for k in xrange(0, n + 1)]
    a.reverse()
    return a</pre></p> 

Note que esta função requer o cálculo do binômio \(\binom{n}{k} \) . A função que faz esta computação é

<pre lang="python">def binomial_coefficients(n, k):
    """
    Calcule any binomial coefficients.

    coeff = binomial coefficients(n, k)

    INPUT:
      * n: power of binomial
      * k: coefficient of x^k term

    return: binomial coefficient

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    fun = lambda i: (n - i + 1.0) / i
    l = [1.0] + [fun(i) for i in xrange(1, k + 1)]
    coeff = reduce(mul, l)
    return coeff</pre></p> 

&nbsp;

### 3.2. Computando as Raízes do Polinômio de Legendre 

O próximo passo é obter as raízes \(a_j \) do polinômio de Legendre. Para isso, precisamos de um algoritmo que calcule as \(n \) raízes de um polinômio de ordem \(n \) . Nesse caso, podemos utilizar qualquer método numérico que realize esta tarefa: Aberth, Bairstow, Laguerre, Jenkins-Traub, etc. 

Como apresentado em outros posts, cada um desses métodos possui vantagens e desvantagens, tais como requerer ou não derivadas, complexidade, etc. Sabendo que todas as raízes do polinômio de Legendre estão definidas no intervalo \([-1,1] \) e sabendo os coeficientes do polinômio, o que nos permite derivá-lo, escolhemos o método de Aberth. Esse método possui uma convergência quadrática e requer a função (polinômio) e a sua derivada. Assim, podemos computar todas as raízes do polinômio utilizando a seguinte função:

<pre lang="python">def compute_legendre_roots(n):
    """
    Compute all roots of the nth Legendre polynomial

    [roots] = compute_legendre_roots(n)

    INPUT:
      * n: order of Legendre polynomial

    return: the roots of P_n(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    legendre_coefficients = compute_legendre_polynomials_coeficients(n)
    diff_coefs = polynomial_derivative_coefficients(legendre_coefficients)
    legendre_fun = polynomial_coeffs_to_function(legendre_coefficients)
    diff_legendre_fun = polynomial_coeffs_to_function(diff_coefs)
    roots = aberth(legendre_fun, diff_legendre_fun, polDegree=n)
    return roots</pre>

Onde _polynomial\_derivative\_coefficients_ realiza a derivada de um polinômio representado como lista e retorna o outro polinômio derivado também em forma de lista:

<pre lang="python">def polynomial_derivative_coefficients(coeff):
    """
    Compute the derivative of a polynomial represented by a list.

    [diff_coefficients] = polynomial_derivative_coefficients(coeff)

    INPUT:
      * coeff: coefficients of the polynomial

    return: a list containing the polynomial coefficients of the derivated
            polynomial (ordered from the highest to lowest)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    order = len(coeff) - 1
    f = lambda i: (order - i) * coeff[i]
    diff = [f(i) for i in xrange(order)]
    return diff</pre></p> 

A função _polynomial\_coeffs\_to_function_ converte uma representação em forma de lista em uma função avaliável em qualquer ponto:

<pre lang="python">def polynomial_coeffs_to_function(coeff):
    """
    Convert the polynomial coefficients in a polynomial function.

    function = polynomial_coeffs_to_function(coeff)

    INPUT:
      * coeff: coefficients of the polynomial

    return: a function

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    order = len(coeff) - 1
    f = lambda x: sum([coeff[i] * x ** (order - i) for i in xrange(order + 1)])
    return f</pre></p> 

&nbsp;

### 3.3. Computando os Pesos da Quadratura 

Conforme a função apresentada, os \(n \) pesos obtidos a partir das \(n \) raízes são calculados pela seguinte função:

<pre lang="python">def compute_quadrature_weights(n):
    """
    Compute the weights of each coefficient used in gaussian quadrature.

    [weights] = compute_quadrature_weights(n)

    INPUT:
      * n: order of Legendre polynomial

    return: a list with the weights

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    def get_diff_Legendre_n(n):
        l1 = compute_legendre_polynomials_coeficients(n)
        diff_coefs = polynomial_derivative_coefficients(l1)
        return polynomial_coeffs_to_function(diff_coefs)

    def compute_weights(n):
        p1n = get_diff_Legendre_n(n)
        a = compute_legendre_roots(n)
        h = lambda i: 2.0 / ((1.0 - a[i] * a[i]) * p1n(a[i]) * p1n(a[i]))
        H = [h(j) for j in xrange(n)]
        return H

    return compute_weights(n)</pre></p> 

&nbsp;

### 3.4. Computando a Integral 

O último passo é computar a integral da função escolhida utilizando a quadratura de Gauss-Legendre:

<pre lang="python">def integral_gaussian_quadrature(fun, xi, xe, order=10):
    """
    Numerical integration using Gaussian quadrature

    integral = integral_gaussian_quadrature(fun, xi, xe, order=10)

    INPUT:
      * fun: function to be integrated
      * xi: beginning of integration interval
      * xe: end of integration interval
      * order: degree of Legendre polynomial

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    def convert_intervals():
        frac = (xe - xi) / 2.0
        xd = lambda x: (xe + xi + (xe - xi) * x) / 2.0
        f = lambda x: fun(xd(x)) * frac
        return f

    def compute_quadrature():
        f = convert_intervals()
        roots = compute_legendre_roots(order)
        weights = compute_quadrature_weights(order)
        approx = lambda i: weights[i] * f(roots[i].real)
        quad = [approx(i) for i in xrange(order)]
        return sum(quad)

    integral = compute_quadrature()
    return integral</pre>

Onde _convert_intervals_ realiza uma mudança de variáveis para converter um intervalo qualquer para o intervalo compatível com o da integral demonstrada no método, isto é, \([-1,1] \) . 

Um exemplo de utilização dessas funções pode ser obtido em <a href="http://www.sawp.com.br/code/integral/integral_gauss_legendre_quadrature.py" target="_blank">http://www.sawp.com.br/code/integral/integral_gauss_legendre_quadrature.py</a>.

&nbsp;

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a>
  </p>
  
  <p>
    <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p></p>
</fieldset>
