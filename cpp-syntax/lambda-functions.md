# Lambda Functions in C++

Anonymous inline function, defined right where needed.

## Syntax

    auto name = [capture](params) -> return_type {
        return statement;
    };

`[]` no capture | `[=]` capture by value | `[&]` capture by reference | `[x, &y]` mixed

## Examples

    auto sum = [](int a, int b) { return a + b; };
    sum(3, 5); // 8

    int factor = 10;
    auto mul = [factor](int x) { return x * factor; };
    mul(4); // 40

    sort(v.begin(), v.end(), [](int a, int b) { return a > b; }); // descending

## CP uses

- Custom comparators (sort, priority_queue)
- Inline callbacks (count_if, accumulate)
- Recursive lambdas via function<> wrapper
