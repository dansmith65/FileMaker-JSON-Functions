Recursion Notes
===============

This file serves as a collection of observations I've made on writing recursive custom functions in FileMaker.


FileMaker Documentation
-----------------------

Recursion limit for custom function:

* 50,000 recursive calls total
* The call stack is only allowed to be 10,000 calls deep at any point. If these limits are violated, the custom function will return "?".
* Note that tail-recursion is properly optimized, so tail calls do not increase the size of the call stack.


Observations
------------

###### Tail recursion allows a maximum depth of 49,999.

```
/**
 * test ( iteration )
 *
 * test ( 0 ) = "?"
 * test ( 1 ) = 49999
 */

If ( iteration >= 49999 ;
	iteration ;
	test ( iteration + 1 )
)
```


###### Saving the result to a variable prevents tail recursion and limits the maximum iterations to 10,000.

```
/**
 * test ( iteration )
 *
 * test ( 0 ) = "?"
 * test ( 1 ) = 10000
 */

If ( iteration >= 10000 ;
	iteration ;
	Let ( [
		result = test ( iteration + 1 )
	] ;
		result
	)
)
```


<a name="3">letVaraibles, $localVariables, and $$globalVariables can still be used with tail recursion, though.</a>

```
/**
 * test ( iteration )
 *
 * test ( 0 ) = "?"
 * test ( 1 ) = 49999
 */

If ( iteration >= 49999 ;
	iteration ;
	Let ( [
		letVaraible = iteration ;
		$localVariable = letVaraible ;
		$$globalVariable = $localVariable
	] ;
		test ( $$globalVariable + 1 )
	)
)
```


<a name="4">Nested Let statements can be used with tail recursion as well.</a>

```
/**
 * test ( iteration )
 *
 * test ( 0 ) = "?"
 * test ( 1 ) = 49999
 */

If ( iteration >= 49999 ;
	iteration ;
	Let ( [
		letVaraible = iteration
	] ;
		Let ( [
			$localVariable = letVaraible
		] ;
			Let ( [
				$$globalVariable = $localVariable
			] ;
				test ( $$globalVariable + 1 )
			)
		)
	)
)
```


<a name="5">A recursive sub-function does not "free up" it's recursive calls once it returns it's result to the calling function. In other words; there is no way to go beyond 50,000 recursive calls.</a>

```
/**
 * test ( iteration )
 *
 * test ( 0 ) = "?"
 * test ( 1 ) = 49991
 */

If ( iteration >= 49991 ;
	iteration ;
	test ( iteration + 1 + testSub ( 1 ) )
)

/**
 * testSub ( iteration )
 */

If ( iteration >= 4998 ;
	iteration ;
	testSub ( iteration + 1 )
)
```


<a name="6">Non-recursive sub-function also uses up recursive calls.</a>

```
/**
 * test ( iteration )
 *
 * test ( 0 ) = "?"
 * test ( 1 ) = 25000
 */

If ( iteration >= 25000 ;
	iteration ;
	test ( testSub ( iteration ) + 1 )
)

/**
 * testSub ( iteration )
 * (all this function does is return it's parameter)
 */

iteration
```


<a name="7">The more sub-functions you access, the less recursion depth you get in the calling function.</a>

```
/**
 * test ( iteration )
 *
 * test ( 0 ) = "?"
 * test ( 1 ) = 16667
 */

If ( iteration >= 16667 ;
	iteration ;
	test (
		testSub ( iteration )
		+ testSub ( 1 )
	)
)

/**
 * testSub ( iteration )
 * (all this function does is return it's parameter)
 */

iteration
```

```
/**
 * test ( iteration )
 *
 * test ( 0 ) = "?"
 * test ( 1 ) = 6250
 */

If ( iteration >= 6250 ;
	iteration ;
	test (
		testSub ( iteration )
		+ testSub ( 1 )
		+ testSub ( 0 )
		+ testSub ( 0 )
		+ testSub ( 0 )
		+ testSub ( 0 )
		+ testSub ( 0 )
	)
)

/**
 * testSub ( iteration )
 * (all this function does is return it's parameter)
 */

iteration
```


<a name="8">Be careful how sub-functions are referenced, or they will prevent tail recursion:</a>

```
/**
 * test ( iteration )
 *
 * test ( 0 ) = "?"
 * test ( 1 ) = 10000
 */

If ( iteration >= 10000 ;
	iteration ;
	test ( iteration + 1 ) & testSub ( "" )
)

/**
 * testSub ( iteration )
 * (all this function does is return it's parameter)
 */

iteration
```
