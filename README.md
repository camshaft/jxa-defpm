jxa-defpm
=========

Declare a multi-clause function, similar to erlang.

## Example:

```erlang
fn(1, dollar) ->
  '$1';
fn(_Amount, _Currency) ->
  too_high.
```

```joxa
(defpm+ fn
 ((1 :dollar)
  :$1)
 ((_amount _currency)
  :too_high))
```

which ends up getting expanded to

```joxa
(defn+ fn (a b)
 (case [a b]
  ([1 :dollar]
   :$1)
  ([_amount _currency]
   :too_high)))
```

`when` clauses are also valid

```joxa
(defpm+ hello
 ((name)
   (when (erlang/is_list name))
  (io/format "hello ~s~n" [name]))
 ((name)
  (io/format "goodbye ~p~n" [name])))
```
