
## 1. Configuration Structure
Configurations are passed as JSON objects and typically include keys such as `key`, `value`, `operator`, and may include nested conditions for complex logic.

### General Structure
```json
{
  "key": "path.to.property",
  "value": "value_to_compare",
  "operator": "comparison_operator"
}
```

### Example
```json
{
  "key": "user.age",
  "value": 30,
  "operator": ">"
}
```

### Nested Conditions for Compound Logic
For complex configurations, `value` can be an array of condition objects, and `operator` can be either `AND` or `OR`.
```json
{
  "value": [
    { "key": "user.age", "value": 18, "operator": ">=" },
    { "key": "user.status", "value": "active", "operator": "==" }
  ],
  "operator": "AND"
}
```

---

## 2. Fields in Configuration

### a. `key`
- **Type**: `string | null`
- **Description**: The key path in the `data` object to retrieve the value for comparison. Can be a nested path like `"user.age"`.
- **Special Case**: If `key` is `null` or not defined, the condition is treated as a compound condition with multiple sub-conditions.

### b. `value`
- **Type**: `any | Array`
- **Description**: The value to compare against the value retrieved from `data` using `key`. If the condition is compound, `value` is an array of sub-conditions.
- **Notes**: Strings `"null"` and `"undefined"` are converted to `null`.

### c. `operator`
- **Type**: `string`
- **Description**: The operator used for comparison. Can be a standard comparison operator or a logical operator for compound conditions.

---

## 3. Supported Operators

### Comparison Operators
- **`>`**: Greater than
- **`<`**: Less than
- **`<=`**: Less than or equal to
- **`>=`**: Greater than or equal to
- **`==`**: Equal (loose comparison, allows type coercion)
- **`===`**: Strictly equal (no type coercion)
- **`!=`**: Not equal (loose comparison)

**Usage Example**:
```json
{ "key": "order.amount", "value": 100, "operator": ">" }
```

### Logical Operators
- **`AND`**: All conditions in the `value` array must be `true`.
- **`OR`**: At least one condition in the `value` array must be `true`.

**Usage Example**:
```json
{
  "key": null,
  "value": [
    { "key": "order.status", "value": "shipped", "operator": "==" },
    { "key": "order.total", "value": 50, "operator": ">" }
  ],
  "operator": "OR"
}
```

---

## 4. Evaluation Logic
The Configuration Manager uses the `evaluate` function to process conditions based on the `key`, `value`, and `operator`.

### Evaluation Steps
1. **Retrieve Value**: The `key` is used to access the corresponding value in the `data` object.
2. **Apply Operator**: The value from `data` is compared with the `value` from the condition using the specified `operator`.
3. **Handle Compound Conditions**:
   - If `value` is an array, the `AND` or `OR` logical operator is used to combine results from all sub-conditions.
4. **Return Result**: The final result is a boolean indicating whether the condition(s) are met.

---

## 5. Handling `null` and `undefined`
- **Automatic Conversion**: The strings `"null"` and `"undefined"` in the `value` field are automatically converted to `null`.
- **Safe Access**: The `getValue` utility function ensures that accessing deeply nested properties does not result in errors if a key is missing.

---

## 6. Example Configurations

### Simple Condition
```json
{
  "key": "user.age",
  "value": 25,
  "operator": "=="
}
```
**Explanation**: Checks if `user.age` is equal to 25.

### Range Check
```json
{
  "key": "product.price",
  "value": 100,
  "operator": "<="
}
```
**Explanation**: Checks if `product.price` is less than or equal to 100.

### Compound Condition with `AND`
```json
{
  "key": null,
  "value": [
    { "key": "account.active", "value": true, "operator": "===" },
    { "key": "account.balance", "value": 0, "operator": ">" }
  ],
  "operator": "AND"
}
```
**Explanation**: Checks if `account.active` is `true` and `account.balance` is greater than 0.

### Compound Condition with `OR`
```json
{
  "key": null,
  "value": [
    { "key": "user.role", "value": "admin", "operator": "==" },
    { "key": "user.accessLevel", "value": 5, "operator": ">=" }
  ],
  "operator": "OR"
}
```
**Explanation**: Checks if `user.role` is "admin" or `user.accessLevel` is greater than or equal to 5.

---

## 7. Utility Function: `getValue`
The `getValue` function is used internally to retrieve the value of a key path from an object safely, even if the path is nested.

### Functionality
- **Input**: An object, a key path, and an index to start the search.
- **Output**: The value at the specified key path or `null` if the path does not exist.

---

This reference document provides a comprehensive understanding of the Configuration Manager, how to set up conditions in JSON, and how they are evaluated. Use it as a guide to configure and manage your conditions effectively.