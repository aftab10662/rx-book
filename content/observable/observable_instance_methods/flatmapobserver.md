## [`Rx.Observable.prototype.flatMapObserver(onNext, onError, onCompleted, [thisArg])`, `Rx.Observable.prototype.selectManyObserver(onNext, onError, onCompleted, [thisArg])`](https://github.com/Reactive-Extensions/RxJS/blob/master/src/core/linq/observable/selectmanyobserver.js)

Projects each notification of an observable sequence to an observable sequence and merges the resulting observable sequences into one observable sequence.

#### Arguments
1. `onNext` *(`Function`)*:  A transform function to apply to each element. The selector is called with the following information:
    1. the value of the element
    2. the index of the element
2. `onError` *(`Function`)*: A transform function to apply when an error occurs in the source sequence.
3. `onCompleted` *(`Function`)*: A transform function to apply when the end of the source sequence is reached.
4. `[thisArg]` *(`Any`)*: Object to use as `this` when executing the transform functions.

#### Returns
*(`Observable`)*: An observable sequence whose elements are the result of invoking the one-to-many transform function corresponding to each notification in the input sequence.

#### Example
```js
var source = Rx.Observable.range(1, 3)
    .flatMapObserver(
        function (x, i) {
            return Rx.Observable.repeat(x, i);
        },
        function (err) {
            return Rx.Observable.return(42);
        },
        function () {
            return Rx.Observable.empty();
        });

var subscription = source.subscribe(
    function (x) {
        console.log('Next: ' + x);
    },
    function (err) {
        console.log('Error: ' + err);
    },
    function () {
        console.log('Completed');
    });

// => Next: 2
// => Next: 3
// => Next: 3
// => Completed
```