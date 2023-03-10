# Array Destructuring

This is an ES6 feature that allows you break a complex data structure like array into a smaller data structure like the array.

# Spread Operator

The spread operator (...) is used to quickly copy all or part of an existing array or object into another array or object.

The spread operator is a bit similar to destructuring; it allows you handle complex arrays and break it down into smaller arrays. t

Difference between the spread operator and destructuring is that spread operators does not create new variables. It can only be used in places where values are seperated by commas.

For instance, you can't use it in a template literal like the example below. This is because the literal expects a single value and not an array of values.

```js
const data = [1, 2, 3, 4];
const [a, b, c, d] = [...data];
console.log(a, b, c, d);
console.log(...data);
```

Another use case of the spread operator is for passing in multiple values into a function.

# Rest Pattern and Parameters

The rest pattern is the opposite of the spread operator. It uses the exact same syntax, however, it it used to collect multiple elements and condense them into an array, whereas, the spread operator is used for unpacking an array into multiple elements or array.

### 1. Rest: Destructuring

Here's an example of the spread operator below. We know we're working with the spread syntax because it is declared on the right side of the assignment operator `=`.

```js
// SPREAD: Because [...] is on the right side of assignment operator =
const arr = [1, 2, ...[3, 4]];
```

We can also use it on the left side along with destructuring. For Example:

```js
// REST: Because [...] is on the left side of assignment operator =
const [a, b, ...others] = [1, 2, 3, 4, 5];
console.log(a, b, others);
```

The output will be `1 2 [3 4 5]` because 1 and 2 will be stored in the a and b variables and then the rest of the value will be stored together in a new array.

This is where the name; Rest is coined from. It collects the elements that are unused in a destructuring assignment.

We can also have the `[...]` dots on both side of the operator.

```js
const [pizza, , risotto, ...otherFood] = [
  ...restaurant.mainMenu,
  ...restaurant.starterMenu,
];

console.log(pizza, risotto, otherFood);
```

Here we stored the value of Pizza and Risotto into two new variables `pizza, risotto` and then the rest of the `(...restaurant.mainMenu and ...restaurant.starterMenu)` array was stored into a new array called `otherFood`.

> **NOTE**
> It's good to remember that the rest pattern should always be the last element in a destructuring assignment otherwise JavaScript will not know what till when it should collect the rest of an array.

For example: You Cannot Do This!

```js
const [pizza, , risotto, ...otherFood, bread]
```

The rest pattern will have to be the last element in other for the operation to work. As a result of this, there can only be one rest pattern in any destructuring assignment.

### Rest in Objects

Just like the spread operator, the rest operator also works on objects.

### 1. Rest: Functions

Just like the spread operator that allows passing in multiple values in a function all at once, the rest operator can do the opposite.

```js
const add = function (...numbers) {
  console.log(numbers);
};

add(2, 3);
add(5, 3, 7, 2);
add(8, 2, 5, 3, 2, 1, 4);
```

### Finally!

The subtle distinction that tells you when and where to use spread and rest.

- Use Spread when you want to write values seperated by commas.
- Use Rest when you want to write variable names seperated by commas.

# Short Circuting (&& and ||)

In the past, we've looked at the `&&` and `||` operators but we only crossed the surface. In this section, we'll look at how to use these operators for something called circuting.

### Properties of logical operators

1. They can use any data type
2. They can return any data type
3. They can perform short circuting (aka short circuit evaluation)

### Short Circuting Or ||

For example:

```js
console.log(3 || "Eke");
```

In the case of the OR operator, short circuting means that if the first operand is a truthy value, it will return that value and not even evaluate the other value.

```js
console.log("????Short Circuting????");
console.log(3 || "Eke");
console.log("" || "Eke");
console.log(true || 0);
console.log(undefined || null);
console.log(undefined || 0 || "" || "Hello" || 23 || null);
```

From the example above, we can see that the result of the OR operator doesn't have to be a boolean. It will simply short circut the entire operation and return the first truthy value.

```js
restaurant.numGuests = 23;
const guest = restaurant.numGuests ? restaurant.numGuests : 10;
console.log(guest);

// In the example above before numGuest was assigned the number 23, restaurant.numGuest was undefined, which makes it a falsy value. And as such the operand will skip to the next value which is 10.

// Instead of using a tenary operator, we can use short-circuting in the OR operator.

const guest2 = restaurant.numGuests || 10;
console.log(guest2);
```

### Short Circuting And &&

Short circuting the And operator works exactly the opposite of the OR operator. This means that if the first operand is a falsy value, it will return that value and not evaluate the other operand.

For Example

```js
// Short Circuting (AND &&)
console.log(0 && "Eke");
console.log(7 && "Eke");

console.log("Hello" && 23 && null && "Eke");

if (restaurant.orderPizza) {
  restaurant.orderPizza("Mushrooms", "Spinach");
}

restaurant.orderPizza && restaurant.orderPizza("Mushrooms", "Spinach");
```

In summary:

- The OR operator will return the first truthy value of all the operands or simply return the last value if all the operands are falsy.

- The AND operator will return the first falsy value or the last value if all the operands are truthy.

In practical real world examples, the OR operator can be used for setting default values and the AND operator for setting executing code in the second operand if the first operand is true.

# The Nullish Coalescing Operator ()

In the example below, the result for the OR operation will be 10 because the first value `restaurant.numGuests` is a truthy value, but if `restaurant.numGuets` becomes 0(a falsy value), the result will 20, the second option in the OR operation.

```js
restaurant.numGuests = 10;
const guests = restaurant.numGuests || 20;
console.log(guests);
```

In other to fix this issue, JavaScript introduced a new property called "The Nullish Coalescing Operator" that is similar to the OR operator.

```js
const guestCorrect = restaurant.numGuests ?? 20;
console.log(guestCOrrect);
```

This works because the Nullish operator works with the concept of Nullish values instead of falsy values. So it works with `Undefined` and `Null` as falsy values and considers empty string and 0 as truthy values.

In other words, the condition will work only if the first value is null or undefined. Since 0 is not a falsy value in the Nullish Coalescing operator, the condition will move to the next option.
