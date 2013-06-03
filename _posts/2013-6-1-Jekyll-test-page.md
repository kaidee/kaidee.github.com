---
layout: post
title: "Jekyll test page"
category: test
tags: [Jekyll, test]
---
## this is a image

{% highlight scheme %}
(define double (lambda (x) (+ x x)))
(double 12)            ; return 24
(double (* 3 4))       ; return 24
(define x 3)
(begin
  (set! x (+ x 1))
  (+ x x))             ; 返回结果 8
(define (abss n)
    (if (< n 0)
        (- 0 n)
        n))
(abss -12)
;sss
{% endhighlight %}
![](/images/usercolor.png)
<pre>
	(define double (lambda (x) (+ x x)))
	(double 12)            ; return 24
	(double (* 3 4))       ; return 24
	(define x 3)
	(begin
	  (set! x (+ x 1))
	  (+ x x))             ; 返回结果 8

	(define (abss n)
	    (if (< n 0)
	        (- 0 n)
	        n))
	(abss -12)
	;sss
</pre>

{% highlight java %}
public class HelloWorld {
    public static void main(String args[]) {
      System.out.println("Hello World!");
    }
}
{% endhighlight %}