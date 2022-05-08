# Chapter3
* variables are saved to the ENV, when execute code, find variable from ENV first, and then use it for the code.
* ways to observe working code:
~~~racket
(require "top.scm")
(run "let f = proc (x) -(x,1) in (f 30)")


(require "lang.scm")
(scan&parse "let f = proc (x) -(x,1) in (f 30)")

(require "interp.scm")
(define parsed (a-program (let-exp 'f (proc-exp 'x (diff-exp (var-exp 'x) (const-exp 1))) (call-exp (var-exp 'f) (const-exp 30)))))


(define inner-parsed (let-exp 'f (proc-exp 'x (diff-exp (var-exp 'x) (const-exp 1))) (call-exp (var-exp 'f) (const-exp 30))))

(require "environments.scm")
(value-of inner-parsed (init-env))
(value-of (proc-exp 'x (diff-exp (var-exp 'x) (const-exp 1))) (init-env))

~~~
* the args of procedure would be extend to env first, it will fetch the args in env by the time of executing the body of a procedure.
* explained the static properties and lexical scoping.
* how to implement flatten variables to env.


# chapter4
~~~racket
(require "top.scm")
(run "let x = newref(17) in deref(x)")
~~~
IMPLICIT-REFS: Locations are created with each binding operation: at each procedure call,
let, or letrec.

